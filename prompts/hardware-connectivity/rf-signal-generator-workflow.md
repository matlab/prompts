---
title: RF Signal Generator Workflow
description: Connect, configure, and generate IQ waveforms using Quick-Control RF Signal Generator (rfsiggen)
tags: [matlab, instrument, rf-instrument, signal-generator, keysight, rohde-schwarz, quick-control, rfsiggen, instrument-control-toolbox]
release: R2017b+
notes:
---

# RF Signal Generator Workflow

Connect, configure, and generate IQ waveforms using the Quick-Control RF Signal Generator (`rfsiggen`) interface from the Instrument Control Toolbox.

## Metadata

- **Tags:** `matlab` `instrument` `rf-instrument` `signal-generator` `keysight` `rohde-schwarz` `quick-control` `rfsiggen` `instrument-control-toolbox`
- **MATLAB Release:** R2017b+
- **Required Toolboxes:** Instrument Control Toolbox™

## The Prompt

```text
Create a MATLAB script to connect, configure, generate and transmit RF signal using a RF Signal Generator Instrument.

Steps:
1. Use the quick control RF Signal Generator interface from Instrument Control Toolbox™.
2. Discover and list out available RF resources and drivers using quick control RF Signal Generator interface capabilities.
3. Connect to the [INSTRUMENT_VENDOR] RF Signal Generator instrument.
4. Provide effective error handling and messaging if the correct driver or instrument resource is not present.
5. Once connected, provide IQ Data as [IQ_DATA] and provide Sample Rate as [FREQUENCY] Hz.
6. Using the above IQ Data and Sample rate, download the waveform for transmission using the `download()` function for the `rfsiggen` interface.
7. Set other RF Signal Generator Parameters:
    a. Center Frequency: [CENTER_FREQUENCY] Hz.
    b. Output Power: [OUTPUT_POWER] dBm.
    c. Loop Count: Infinity for continuous transmission.
8. Start the signal generation using the above parameters.
9. Disconnect and perform resource cleanup.

Additional Configurations:
- IQ_DATA: [IQ_DATA_DESCRIPTION]
```

## Usage Tips

1. **Specify instrument vendor and model:** Include the vendor and model in the prompt so the generated code selects the correct instrument resource and driver.
2. **Add safety validation:** Optionally add the following prompt to validate instrument safety before transmission:
    ```text
    Validate Instrument Safety, ensuring that:
    - [CENTER_FREQUENCY] Hz is within [MIN_FREQUENCY] to [MAX_FREQUENCY] Hz range.
    - [OUTPUT_POWER] dBm is within [MIN_POWER] to [MAX_POWER] dBm range before proceeding.
    
    Abort with error message if any parameter exceeds safe operating limits.
    ```
3. **Install required drivers:** Ensure [NI-VISA and IVI Compliance Package](https://www.mathworks.com/matlabcentral/fileexchange/49659-instrument-control-toolbox-support-package-for-national-instruments-visa-and-icp-interfaces) are installed. For instruments other than Keysight or Rohde&Schwarz, install the appropriate [IVI-C driver](https://www.ivifoundation.org/DriverRegistry/DriverRegistry.html) for your instrument.
4. **Describe IQ data clearly:** Provide details about the IQ waveform (number of points, cycles, modulation type) in the `[IQ_DATA_DESCRIPTION]` placeholder for accurate code generation.

## Example Usage

### Example 1: Keysight RF Signal Generator with Custom IQ Waveform

```text
Create a MATLAB script to connect, configure, generate and transmit RF signal using a RF Signal Generator Instrument.

Steps:
1. Use the quick control RF Signal Generator interface from Instrument Control Toolbox™.
2. Discover and list out available RF resources and drivers using quick control RF Signal Generator interface capabilities.
3. Connect to the Keysight RF Signal Generator instrument.
4. Provide effective error handling and messaging if the correct driver or instrument resource is not present.
5. Once connected, provide IQ Data as IQ_DATA and provide Sample Rate as 10e6 Hz.
6. Using the above IQ Data and Sample rate, download the waveform for transmission using the `download()` function for the `rfsiggen` interface.
7. Set other RF Signal Generator Parameters:
    a. Center Frequency: 1e9 Hz.
    b. Output Power: 0 dBm.
    c. Loop Count: Infinity for continuous transmission.
8. Start the signal generation using the above parameters.
9. Disconnect and perform resource cleanup.

Additional Configurations:
IQ_DATA: Create a complex IQ waveform using 1000 points and 101 cycles. Calculate the phase increment, generate I and Q components using cosine and sine functions, combine them into complex IQ data, and format as a row vector. Add comments for each section.
```

## Expected Output

```matlab
%% =========================================================================
% rf_siggen_tx.m
% Connect, configure, generate, and transmit an RF signal using a Keysight
% RF Signal Generator via Instrument Control Toolbox (Quick-Control interface)
%% =========================================================================

clear; clc;

%% ============================ USER PARAMETERS ============================

% Sample Rate (Hz)
SampleRate = 10e6;

% RF Signal Generator Settings
CenterFrequency = 1e9;   % 1 GHz
OutputPower     = 0;      % 0 dBm
LoopCount       = inf;    % Continuous transmission

% If you know your VISA resource, set it here:
% e.g., 'TCPIP0::192.168.1.55::inst0::INSTR'
USER_RESOURCE = "";  % Leave empty to auto-select from discovered list

% Preferred Keysight driver names
PREFERRED_DRIVERS = ["AgRfSigGen", "AgRfSigGen_SCPI", "AgRFSigGen", "AgRFSigGen_SCPI"];

%% =========================== CREATE rfsiggen OBJ =========================

rf = rfsiggen;  % Quick-Control RF SigGen object

%% ==================== DISCOVER RESOURCES & DRIVERS =======================

disp("=== Discovering VISA Resources ===");
resourceList = resources(rf);

disp("=== Discovering Installed RF Drivers ===");
driverList = drivers(rf);

%% ============================== SELECT RESOURCE ==========================

if ~isempty(USER_RESOURCE)
    selectedResource = USER_RESOURCE;
else
    % Auto-pick a resource by prioritizing TCPIP > USB > GPIB > Other
    selectedResource = "";
    r = string(resourceList);

    if any(contains(r, "TCPIP", "IgnoreCase", true))
        selectedResource = r(find(contains(r, "TCPIP", "IgnoreCase", true), 1));
    elseif any(contains(r, "USB", "IgnoreCase", true))
        selectedResource = r(find(contains(r, "USB", "IgnoreCase", true), 1));
    elseif any(contains(r, "GPIB", "IgnoreCase", true))
        selectedResource = r(find(contains(r, "GPIB", "IgnoreCase", true), 1));
    elseif ~isempty(r)
        selectedResource = r(1);
    end

    if strlength(selectedResource) == 0
        error("No VISA instrument resource found. Connect instrument and retry.");
    end
end

fprintf("Selected Resource: %s\n", selectedResource);
rf.Resource = selectedResource;

%% ============================ SELECT DRIVER ==============================

selectedDriver = "";

% Identify first matching Keysight driver from discovered list
for d = PREFERRED_DRIVERS
    if any(contains(string(driverList), d, "IgnoreCase", true))
        selectedDriver = d;
        break;
    end
end

if strlength(selectedDriver) == 0
    error("No Keysight RF SigGen driver found. Install AgRfSigGen or AgRfSigGen_SCPI.");
end

fprintf("Selected Driver: %s\n", selectedDriver);
rf.Driver = selectedDriver;

%% ============================== CONNECT =================================

fprintf("Connecting to RF Signal Generator...\n");
try
    connect(rf);
    disp("Connection successful.");
catch ME
    error("Failed to connect: %s", ME.message);
end

%% ========================== GENERATE IQ WAVEFORM =========================
% Create complex IQ waveform:
% - 1000 points
% - 101 cycles across the record
% - Phase increment = 2*pi*(cycles/points)
% - I = cos(phase), Q = sin(phase)
% - Combine to complex row vector

disp("Generating IQ waveform...");

numPoints = 1000;
numCycles = 101;

% Phase increment
phaseInc = 2*pi*(numCycles/numPoints);

% Sample indices
n = 0:(numPoints-1);

% Phase for each point
phase = n * phaseInc;

% I/Q components
I = cos(phase);
Q = sin(phase);

% Complex IQ Data
IQ_DATA = I + 1j*Q;
IQ_DATA = IQ_DATA(:).';  % Ensure row vector

%% ============================= DOWNLOAD IQ ===============================

fprintf("Downloading IQ waveform (%d points, %.2f MHz)...\n", ...
    numPoints, SampleRate/1e6);

try
    download(rf, IQ_DATA, SampleRate);
    disp("Waveform download complete.");
catch ME
    error("Waveform download failed: %s", ME.message);
end

%% ===================== CONFIGURE & START TRANSMISSION ====================

fprintf("Starting RF Transmission:\n");
fprintf("  Center Frequency : %.3f GHz\n", CenterFrequency/1e9);
fprintf("  Output Power     : %.2f dBm\n", OutputPower);
fprintf("  Loop Count       : %g (continuous)\n", LoopCount);

try
    start(rf, CenterFrequency, OutputPower, LoopCount);
    disp("Transmission started.");
catch ME
    error("Failed to start transmission: %s", ME.message);
end

%% ============================== CLEANUP =================================

cleanupObj = onCleanup(@() cleanupRF(rf));

disp("Script complete. RF generator transmitting continuously...");

%% ===================== LOCAL CLEANUP FUNCTION ============================
function cleanupRF(rf)
    try
        stop(rf);
    catch
    end

    try
        disconnect(rf);
    catch
    end

    try
        delete(rf);
    catch
    end

    fprintf("RF Signal Generator disconnected and cleaned up.\n");
end
```

## Related Prompts

- [Control Function Generator Using VISA Interface](visa-function-generator-control.md) - Control function generators using the visadev SCPI interface

## References

- [MATLAB Documentation: Quick Control Interfaces](https://www.mathworks.com/help/instrument/quick-control-interfaces.html)
- [MATLAB Documentation: rfsiggen](https://www.mathworks.com/help/instrument/rfsiggen.html)
- [MATLAB Documentation: Quick-Control RF Signal Generator Requirements](https://www.mathworks.com/help/instrument/quick-control-rf-signal-generator-requirements.html)
- [MATLAB Documentation: Quick Control Interfaces — Examples](https://www.mathworks.com/help/instrument/examples.html?category=quick-control-interfaces)
- [MATLAB Documentation: Instrument Control Toolbox](https://www.mathworks.com/help/instrument/)
