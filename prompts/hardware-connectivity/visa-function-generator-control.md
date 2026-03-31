---
title: Control Function Generator Using VISA Interface
description: Generate MATLAB code to control function generators using the visadev interface with SCPI commands
tags: [matlab, instrument, visa, function-generator, keysight, rohde-schwarz, scpi, instrument-control-toolbox]
release: R2021a+
notes:
---

# Control Function Generator Using VISA Interface

Generate MATLAB code to control function generators using the `visadev` interface from the Instrument Control Toolbox, covering instrument connection, SCPI command configuration for various waveform types, and robust error handling.

## Metadata

- **Tags:** `matlab` `instrument` `visa` `function-generator` `keysight` `rohde-schwarz` `scpi` `instrument-control-toolbox`
- **MATLAB Release:** R2021a+
- **Required Toolboxes:** Instrument Control Toolbox™

## The Prompt

```text
Generate MATLAB code to control a function generator using the visadev interface from the Instrument Control Toolbox.

Requirements:
- Connect to a [INSTRUMENT_VENDOR] [INSTRUMENT_MODEL] function generator via [INTERFACE_TYPE] interface
- Use the VISA resource address: [RESOURCE_NAME]
- Configure the instrument to generate a [WAVEFORM_TYPE] waveform with the following parameters:
    - Frequency: [FREQUENCY] Hz
    - Amplitude: [AMPLITUDE] Vpp (peak-to-peak voltage)
    - Offset: [DC_OFFSET] V
    - Output impedance: [IMPEDANCE] Ohms
    - [ADDITIONAL_CONFIGURATION]
- Enable the output and verify the configuration
- Include proper error handling and resource cleanup

The code should:
- Use `visadevlist` to verify instrument availability (commented out for reference)
- Create a `visadev` connection object
- Send SCPI commands using `writeline()` or `writeread()`
- Query instrument identification (e.g. `*IDN?`)
- Include comments explaining each configuration step
- Properly close the connection when done
- Generate well-commented, production-ready code suitable for test automation.

**User Input Required - SCPI Manual/Reference**
- SCPI Reference: **[SCPI_REFERENCE]**
- Use only SCPI commands documented in SCPI Reference. Do not assume instrument-specific SCPI syntax if SCPI Reference is not provided.

Generate well-commented, production-ready code suitable for test automation.
```

## Usage Tips

### Finding your VISA resource name

Run `visadevlist` in MATLAB to see all connected instruments and their resource names (e.g., "GPIB0::10::INSTR", "USB0::0x0957::0x2C07::MY52801234::INSTR", "TCPIP0::192.168.1.100::inst0::INSTR")

### SCPI commands

- You need to provide the SCPI manual/Reference in place of **[SCPI_REFERENCE]**
- If your AI tool supports internet access, include the programming manual URL in the prompt.
- If your AI tool supports file-based context, attach the manual directly.
- Alternatively, you can paste the relevant SCPI commands into the prompt.

**SCPI command variations**: Different manufacturers use similar but not identical SCPI commands. Common variations:

- Keysight/Agilent: `SOUR1:FUNC SIN`, `SOUR1:VOLT 1.0`
- Tektronix: `SOURCE1:FUNCTION:SHAPE SIN`, `SOURCE1:VOLTAGE:AMPLITUDE 1.0`
- Consult your instrument's programming manual for exact syntax
- Specify complete requirements: Include output channel (if multi-channel), trigger source, modulation needs, and any synchronization requirements for better code generation

**Interface-specific considerations**:

- GPIB: Specify board index and primary address
- USB: May require instrument-specific drivers installed
- TCP/IP: Include IP address and port (for Socket) or use VXI11/HiSLIP protocols

## Example Usage

### Example 1: Generate Simple Sine Wave (Keysight 33500B)

```text
Generate MATLAB code to control a function generator using the `visadev` interface from the Instrument Control Toolbox.

Requirements:
1. Connect to a Keysight 33522B function generator via GPIB interface
2. Use the VISA resource address: `GPIB0::10::INSTR`
3. Configure the instrument to generate a sine wave waveform with the following parameters:
    - Frequency: 1000 Hz
    - Amplitude: 2.0 Vpp (peak-to-peak voltage)
    - Offset: 0 V
    - Output impedance: 50 Ohms
4. Set the output load to 50 Ohms
5. Enable the output and verify the configuration
6. Include proper error handling and resource cleanup

**User Input Required - SCPI Manual/Reference**
- SCPI Reference: https://www.keysight.com/us/en/assets/9018-03714/service-manuals/9018-03714.pdf
- Use only SCPI commands documented in SCPI Reference. Do not assume instrument-specific SCPI syntax if SCPI Reference is not provided.

The code should:
- Use `visadevlist` to verify instrument availability (commented out for reference)
- Create a `visadev` connection object
- Send SCPI commands using `writeline()` or `writeread()`
- Query instrument identification (`*IDN?`)
- Include comments explaining each configuration step
- Properly close the connection when done

Generate well-commented, production-ready code suitable for test automation.
```

### Example 2: Frequency Sweep for Bode Plot

```text
Generate MATLAB code to control a function generator using the `visadev` interface from the Instrument Control Toolbox.

Requirements:
1. Connect to a Tektronix AFG3102 function generator via USB interface
2. Use the VISA resource address: `USB0::0x0699::0x0346::C012345::INSTR`
3. Configure the instrument to generate a swept sine wave waveform with the following parameters:
    - Start frequency: 10 Hz
    - Stop frequency: 10000 Hz
    - Amplitude: 1.0 Vpp (peak-to-peak voltage)
    - Offset: 0 V
    - Output impedance: High-Z (1 MOhm)
4. Configure linear sweep mode with 5 second sweep time
5. Set trigger source to immediate (free run)
6. Enable the output and verify the configuration
7. Include proper error handling and resource cleanup

**User Input Required - SCPI Manual/Reference**
- SCPI Reference: https://download.tek.com/manual/AFG3000-Series-Arbitrary-Function-Generator-Programmer-EN.pdf
- Use only SCPI commands documented in SCPI Reference. Do not assume instrument-specific SCPI syntax if SCPI Reference is not provided.

The code should:
- Use `visadevlist` to verify instrument availability (commented out for reference)
- Create a `visadev` connection object
- Send SCPI commands using `writeline()` or `writeread()`
- Query instrument identification (`*IDN?`)
- Include comments explaining each configuration step
- Properly close the connection when done

Generate well-commented, production-ready code suitable for test automation.
```

### Example 3: Arbitrary Waveform Generation

```text
Generate MATLAB code to control a function generator using the `visadev` interface from the Instrument Control Toolbox.

Requirements:
1. Connect to a Keysight 33600A function generator via TCP/IP interface using HiSLIP protocol
2. Use the VISA resource address: `TCPIP0::192.168.1.100::hislip0::INSTR`
3. Configure the instrument to generate an arbitrary waveform with the following parameters:
    - Create a custom waveform: damped sinusoid (sine wave with exponentially decaying amplitude)
    - Sample rate: 1 MSa/s
    - Waveform frequency: 500 Hz
    - Amplitude: 3.0 Vpp
    - Offset: 0 V
    - Output impedance: 50 Ohms
4. Download the arbitrary waveform data to the instrument's volatile memory
5. Configure the instrument to output this arbitrary waveform
6. Enable the output and verify the configuration
7. Include proper error handling and resource cleanup

**User Input Required - SCPI Manual/Reference**
- SCPI Reference: https://www.keysight.com/us/en/assets/9018-03714/service-manuals/9018-03714.pdf
- Use only SCPI commands documented in SCPI Reference. Do not assume instrument-specific SCPI syntax if SCPI Reference is not provided.

The code should:
- Use `visadevlist` to verify instrument availability (commented out for reference)
- Create a `visadev` connection object
- Generate the arbitrary waveform data in MATLAB
- Send SCPI commands using `writeline()` or `writeread()`
- Transfer binary waveform data using `writebinblock()`
- Query instrument identification (`*IDN?`)
- Include comments explaining each configuration step
- Properly close the connection when done

Generate well-commented, production-ready code suitable for test automation.
```

## Expected Output

```matlab
% Connect to [Instrument Model] function generator
% Resource: [Resource Name]

% Uncomment to list available VISA resources
% resourceList = visadevlist;
% disp(resourceList);
try
  % Create VISA connection
  fgen = visadev("[RESOURCE_NAME]");

  % Query instrument identification
  idn = writeread(fgen, "*IDN?");
  fprintf('Connected to: %s\n', idn);

  % Reset instrument to known state
  writeline(fgen, "*RST");
  writeline(fgen, "*CLS");

  % Configure waveform parameters
  writeline(fgen, "[FUNCTION_COMMAND]");  % Set waveform type
  writeline(fgen, "[FREQUENCY_COMMAND]"); % Set frequency
  writeline(fgen, "[AMPLITUDE_COMMAND]"); % Set amplitude
  writeline(fgen, "[OFFSET_COMMAND]");    % Set DC offset

  % Configure output settings
  writeline(fgen, "[OUTPUT_LOAD_COMMAND]");

  % Enable output
  writeline(fgen, "[OUTPUT_ON_COMMAND]");

  % Verify configuration (optional)
  config = writeread(fgen, "[QUERY_COMMAND]");
  fprintf('Configuration: %s\n', config);

  % Check for any system errors
  errorQuery = writeread(fgen, "SYSTem:ERRor?");
  fprintf("\nSystem Error Check: %s\n", errorQuery);
  if contains(errorQuery, "+0") || contains(errorQuery, "No error")
     fprintf("\n✓ Configuration completed successfully!\n");
     fprintf("Sine wave is now being generated on Output 1.\n");
  else
     warning("System reported an error: %s", errorQuery);
  end
  catch ME
  % ---------------------------------------------------------------------
  % Error Handling
  % ---------------------------------------------------------------------
   fprintf("\n ERROR: %s\n", ME.message);
   fprintf("Error occurred in: %s\n", ME.stack(1).name);
   fprintf("At line: %d\n", ME.stack(1).line);
end

% Clean up
clear fgen;
fprintf('Function generator configured successfully.\n');
```

## Common Patterns

```matlab
% Pattern 1: Basic waveform configuration (standard functions)
writeline(fgen, "SOURce1:FUNCtion SIN");           % Sine wave
writeline(fgen, "SOURce1:FREQuency 1000");         % 1 kHz
writeline(fgen, "SOURce1:VOLTage 2.0");            % 2V p-p
writeline(fgen, "SOURce1:VOLTage:OFFSet 0");       % 0V offset
writeline(fgen, "OUTPut1:LOAD 50");                % 50 Ohm load
writeline(fgen, "OUTPut1 ON");                     % Enable output

% Pattern 2: Sweep configuration
writeline(fgen, "SOURce1:FREQuency:MODE SWEep");
writeline(fgen, "SOURce1:FREQuency:STARt 10");
writeline(fgen, "SOURce1:FREQuency:STOP 10000");
writeline(fgen, "SOURce1:SWEep:SPACing LINear");
writeline(fgen, "SOURce1:SWEep:TIME 5");
```

## Troubleshooting

### Problem: `visadevlist` doesn't show my instrument

Solution: Verify physical connection (cable, power). Check that VISA drivers are installed (NI-VISA, Keysight IO Libraries, or Tektronix OpenChoice). For USB instruments, ensure device drivers are installed. For TCP/IP, verify network connectivity with ping.

### Problem: Error "Unable to connect to instrument"

Solution: Verify the resource name is exactly correct (case-sensitive). Check if another application has the instrument connection open. For GPIB, verify board index and address match your setup. Try increasing the timeout, like `fgen.Timeout = 10;`

### Problem: Commands don't seem to work or return errors

Solution: Check SCPI command syntax in instrument manual. Some instruments require specific command sequencing. Use `writeread(fgen, "SYSTem:ERRor?")` to query instrument error queue. Verify instrument is in remote mode (not local/manual mode).

## Related Prompts

- [RF Signal Generator Workflow](rf-signal-generator-workflow.md) - Control RF signal generators using the Quick-Control rfsiggen interface

## References

- [MATLAB Documentation: visadev](https://www.mathworks.com/help/instrument/visadev.html)
- [MATLAB Documentation: visadevlist](https://www.mathworks.com/help/instrument/visadevlist.html)
- [MATLAB Documentation: Instrument Control Toolbox](https://www.mathworks.com/help/instrument/)
