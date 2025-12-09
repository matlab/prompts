---
title: Create High-Performance Animated Plots
description: Create smooth animations by updating plot data efficiently without recreating graphics objects
tags: [matlab, visualization, animation, performance, drawnow, graphics]
release: All releases
notes:
---

# Create High-Performance Animated Plots

Create smooth, efficient animations by updating existing plot objects rather than recreating them - following MATLAB performance best practices.

## Metadata

- **Tags:** `matlab` `visualization` `animation` `performance` `drawnow` `graphics`
- **MATLAB Release:** All releases
- **Required Toolboxes:** None

## The Prompt

```text
Create an animated MATLAB visualization following these performance best practices:

CRITICAL PERFORMANCE RULES:
1. Create plot objects ONCE before the loop with initial/NaN data
2. Store plot objects as variables (e.g., h = plot(x, y))
3. Inside the loop, UPDATE only XData, YData, ZData properties - DO NOT call plot() again
4. Set axis limits MANUALLY before the loop using xlim(), ylim(), zlim()
5. Use drawnow limitrate (not drawnow) for high-speed animations - limits to 20 fps
6. Call drawnow BEFORE the loop starts to ensure axes are visible
7. Disable interactivity if not needed: disableDefaultInteractivity(ax)
8. Remove toolbar if not needed: ax.Toolbar = []

ANIMATION PATTERN:
    % Step 1: Create figure and axes
    figure;
    ax = axes;
    xlim(ax, [xMin xMax]);
    ylim(ax, [yMin yMax]);
    % Optional: disableDefaultInteractivity(ax);
    % Optional: ax.Toolbar = [];

    % Step 2: Create plot object with initial data
    h = plot(NaN, NaN, 'LineWidth', 2);
    title('Animation Title');
    xlabel('X Label');
    ylabel('Y Label');

    % Step 3: Force initial draw
    drawnow;

    % Step 4: Animation loop - update data only
    for k = 1:numFrames
        % Compute new data
        newX = ...;
        newY = ...;

        % Update plot data (NOT recreate plot)
        h.XData = newX;
        h.YData = newY;

        % Update display with frame rate limit
        drawnow limitrate;
    end

ANIMATION TYPES:
- Line/curve animations (growing traces, moving objects)
- Scatter plot animations (particle systems, data evolution)
- Surface/mesh animations (3D evolving landscapes)
- Multiple object animations (coordinated motion)

Create an animation for: [DESCRIBE YOUR ANIMATION REQUIREMENTS]

Include:
- Initial plot setup with proper limits
- Efficient data update loop
- Optional: pause controls, speed adjustment
- Optional: save as video or GIF
```

## Usage Tips

1. **Specify animation type:** Describe what should be animated (line growing, object moving, data evolving, etc.)
2. **Set duration/frames:** Mention how long the animation should run or how many frames
3. **Define data source:** Explain whether data is computed, loaded from file, or simulated
4. **Request controls:** Ask for pause/resume, speed control, or interactive elements if needed
5. **Output format:** Specify if you need to save as video (MP4, AVI) or GIF

## Example Usage

### Example 1: Growing Sine Wave

```text
Create an animated MATLAB visualization following these performance best practices:

CRITICAL PERFORMANCE RULES:
1. Create plot objects ONCE before the loop with initial/NaN data
2. Store plot objects as variables (e.g., h = plot(x, y))
3. Inside the loop, UPDATE only XData, YData, ZData properties - DO NOT call plot() again
4. Set axis limits MANUALLY before the loop using xlim(), ylim(), zlim()
5. Use drawnow limitrate (not drawnow) for high-speed animations - limits to 20 fps
6. Call drawnow BEFORE the loop starts to ensure axes are visible
7. Disable interactivity if not needed: disableDefaultInteractivity(ax)
8. Remove toolbar if not needed: ax.Toolbar = []

ANIMATION PATTERN:
    % Step 1: Create figure and axes
    figure;
    ax = axes;
    xlim(ax, [xMin xMax]);
    ylim(ax, [yMin yMax]);
    % Optional: disableDefaultInteractivity(ax);
    % Optional: ax.Toolbar = [];

    % Step 2: Create plot object with initial data
    h = plot(NaN, NaN, 'LineWidth', 2);
    title('Animation Title');
    xlabel('X Label');
    ylabel('Y Label');

    % Step 3: Force initial draw
    drawnow;

    % Step 4: Animation loop - update data only
    for k = 1:numFrames
        % Compute new data
        newX = ...;
        newY = ...;

        % Update plot data (NOT recreate plot)
        h.XData = newX;
        h.YData = newY;

        % Update display with frame rate limit
        drawnow limitrate;
    end

ANIMATION TYPES:
- Line/curve animations (growing traces, moving objects)
- Scatter plot animations (particle systems, data evolution)
- Surface/mesh animations (3D evolving landscapes)
- Multiple object animations (coordinated motion)

Create an animation for: A sine wave that grows from left to right over 1000 frames.
Show x from 0 to 2*pi, y = sin(x).
Use a red line with thickness 2.
Add a title showing the current frame number.

Include:
- Initial plot setup with proper limits
- Efficient data update loop
- Optional: pause controls, speed adjustment
- Optional: save as video or GIF
```

### Example 2: Particle System

```text
Create an animated MATLAB visualization following these performance best practices:

CRITICAL PERFORMANCE RULES:
1. Create plot objects ONCE before the loop with initial/NaN data
2. Store plot objects as variables (e.g., h = plot(x, y))
3. Inside the loop, UPDATE only XData, YData, ZData properties - DO NOT call plot() again
4. Set axis limits MANUALLY before the loop using xlim(), ylim(), zlim()
5. Use drawnow limitrate (not drawnow) for high-speed animations - limits to 20 fps
6. Call drawnow BEFORE the loop starts to ensure axes are visible
7. Disable interactivity if not needed: disableDefaultInteractivity(ax)
8. Remove toolbar if not needed: ax.Toolbar = []

ANIMATION PATTERN:
    % Step 1: Create figure and axes
    figure;
    ax = axes;
    xlim(ax, [xMin xMax]);
    ylim(ax, [yMin yMax]);
    % Optional: disableDefaultInteractivity(ax);
    % Optional: ax.Toolbar = [];

    % Step 2: Create plot object with initial data
    h = plot(NaN, NaN, 'LineWidth', 2);
    title('Animation Title');
    xlabel('X Label');
    ylabel('Y Label');

    % Step 3: Force initial draw
    drawnow;

    % Step 4: Animation loop - update data only
    for k = 1:numFrames
        % Compute new data
        newX = ...;
        newY = ...;

        % Update plot data (NOT recreate plot)
        h.XData = newX;
        h.YData = newY;

        % Update display with frame rate limit
        drawnow limitrate;
    end

ANIMATION TYPES:
- Line/curve animations (growing traces, moving objects)
- Scatter plot animations (particle systems, data evolution)
- Surface/mesh animations (3D evolving landscapes)
- Multiple object animations (coordinated motion)

Create an animation for: 50 particles moving in 2D space with random walk motion over 1500 frames.
Use scatter plot with different colors for each particle.
Set axis limits to [-10, 10] for both x and y.
Add trailing paths showing last 20 positions.

Include:
- Initial plot setup with proper limits
- Efficient data update loop
- Optional: pause controls, speed adjustment
- Optional: save as video or GIF
```

### Example 3: 3D Surface Evolution

```text
Create an animated MATLAB visualization following these performance best practices:

CRITICAL PERFORMANCE RULES:
1. Create plot objects ONCE before the loop with initial/NaN data
2. Store plot objects as variables (e.g., h = plot(x, y))
3. Inside the loop, UPDATE only XData, YData, ZData properties - DO NOT call plot() again
4. Set axis limits MANUALLY before the loop using xlim(), ylim(), zlim()
5. Use drawnow limitrate (not drawnow) for high-speed animations - limits to 20 fps
6. Call drawnow BEFORE the loop starts to ensure axes are visible
7. Disable interactivity if not needed: disableDefaultInteractivity(ax)
8. Remove toolbar if not needed: ax.Toolbar = []

ANIMATION PATTERN:
    % Step 1: Create figure and axes
    figure;
    ax = axes;
    xlim(ax, [xMin xMax]);
    ylim(ax, [yMin yMax]);
    % Optional: disableDefaultInteractivity(ax);
    % Optional: ax.Toolbar = [];

    % Step 2: Create plot object with initial data
    h = plot(NaN, NaN, 'LineWidth', 2);
    title('Animation Title');
    xlabel('X Label');
    ylabel('Y Label');

    % Step 3: Force initial draw
    drawnow;

    % Step 4: Animation loop - update data only
    for k = 1:numFrames
        % Compute new data
        newX = ...;
        newY = ...;

        % Update plot data (NOT recreate plot)
        h.XData = newX;
        h.YData = newY;

        % Update display with frame rate limit
        drawnow limitrate;
    end

ANIMATION TYPES:
- Line/curve animations (growing traces, moving objects)
- Scatter plot animations (particle systems, data evolution)
- Surface/mesh animations (3D evolving landscapes)
- Multiple object animations (coordinated motion)

Create an animation for: A 3D surface z = sin(sqrt(x^2 + y^2) - t) evolving over time across 1200 frames.
Set t from 0 to 4*pi.
Use surf() with colormap 'jet'.
Set axis limits to [-5, 5] for x and y, [-1.5, 1.5] for z.
Rotate view angle slightly each frame.

Include:
- Initial plot setup with proper limits
- Efficient data update loop
- Optional: pause controls, speed adjustment
- Optional: save as video or GIF
```

### Example 4: Real-Time Data Simulation

```text
Create an animated MATLAB visualization following these performance best practices:

CRITICAL PERFORMANCE RULES:
1. Create plot objects ONCE before the loop with initial/NaN data
2. Store plot objects as variables (e.g., h = plot(x, y))
3. Inside the loop, UPDATE only XData, YData, ZData properties - DO NOT call plot() again
4. Set axis limits MANUALLY before the loop using xlim(), ylim(), zlim()
5. Use drawnow limitrate (not drawnow) for high-speed animations - limits to 20 fps
6. Call drawnow BEFORE the loop starts to ensure axes are visible
7. Disable interactivity if not needed: disableDefaultInteractivity(ax)
8. Remove toolbar if not needed: ax.Toolbar = []

ANIMATION PATTERN:
    % Step 1: Create figure and axes
    figure;
    ax = axes;
    xlim(ax, [xMin xMax]);
    ylim(ax, [yMin yMax]);
    % Optional: disableDefaultInteractivity(ax);
    % Optional: ax.Toolbar = [];

    % Step 2: Create plot object with initial data
    h = plot(NaN, NaN, 'LineWidth', 2);
    title('Animation Title');
    xlabel('X Label');
    ylabel('Y Label');

    % Step 3: Force initial draw
    drawnow;

    % Step 4: Animation loop - update data only
    for k = 1:numFrames
        % Compute new data
        newX = ...;
        newY = ...;

        % Update plot data (NOT recreate plot)
        h.XData = newX;
        h.YData = newY;

        % Update display with frame rate limit
        drawnow limitrate;
    end

ANIMATION TYPES:
- Line/curve animations (growing traces, moving objects)
- Scatter plot animations (particle systems, data evolution)
- Surface/mesh animations (3D evolving landscapes)
- Multiple object animations (coordinated motion)

Create an animation for: Simulating streaming data like a live oscilloscope over 1500 frames.
Show a scrolling window of 100 points.
Generate random noisy data at each step.
Update at smooth frame rate.
Add grid and axis labels.
Include a pause button.

Include:
- Initial plot setup with proper limits
- Efficient data update loop
- Optional: pause controls, speed adjustment
- Optional: save as video or GIF
```

## Expected Output

The AI will generate optimized animation code like this:

```matlab
% Setup
figure('Position', [100 100 800 600]);
ax = axes;
xlim(ax, [0 2*pi]);
ylim(ax, [-1.5 1.5]);
ax.XLabel.String = 'Time';
ax.YLabel.String = 'Amplitude';
title(ax, 'Animated Sine Wave');
grid(ax, 'on');

% Create initial plot object
h = plot(ax, NaN, NaN, 'r-', 'LineWidth', 2);
drawnow;  % Initial draw

% Animation loop (use 1000+ frames for smooth extended animation)
numFrames = 1000;
for k = 1:numFrames
    % Compute new data
    x = linspace(0, 2*pi*k/numFrames, 100);
    y = sin(x);

    % Update plot data
    h.XData = x;
    h.YData = y;

    % Update display
    drawnow limitrate;
end
```

## Performance Comparison

**Slow (recreates plot each frame):**
```matlab
for k = 1:1000
    plot(x, y);  % Recreates entire plot
    drawnow;
end
```

**Fast (updates data only):**
```matlab
h = plot(NaN, NaN);
for k = 1:1000
    h.XData = x;  % Updates existing object
    h.YData = y;
    drawnow limitrate;  % Caps at 20 fps
end
```

**Note:** Use 1000+ frames for extended animations. Initial frames may render quickly before `drawnow limitrate` stabilizes the frame rate.

## Advanced Features

**Saving animations:**
```matlab
% Create video writer
v = VideoWriter('animation.mp4', 'MPEG-4');
v.FrameRate = 30;
open(v);

% Animation loop
for k = 1:numFrames
    % Update plot...
    drawnow;
    frame = getframe(gcf);
    writeVideo(v, frame);
end
close(v);
```

**Interactive controls:**
```matlab
% Add pause button
uicontrol('Style', 'pushbutton', 'String', 'Pause', ...
    'Position', [20 20 100 40], 'Callback', @pauseCallback);
```

## Best Practices

- **Pre-compute when possible:** Calculate data outside the loop if feasible
- **Use limitrate:** For smooth animations at reasonable frame rates
- **Set fixed limits:** Manual axis limits prevent flickering
- **Profile performance:** Use tic/toc to measure frame update time
- **Consolidate objects:** Use one object with matrix data instead of multiple objects

## Troubleshooting

**Problem:** Animation is choppy or slow
**Solution:** Ensure you're updating XData/YData, not calling plot(). Use drawnow limitrate.

**Problem:** Axes keep resizing during animation
**Solution:** Set xlim, ylim, zlim manually before the loop.

**Problem:** Animation flickers
**Solution:** Call drawnow once before the loop to initialize display.

**Problem:** Frame rate is too fast
**Solution:** Add pause() between frames or use drawnow limitrate.

## Related Prompts

- [Create Custom Multi-Panel Visualizations with Tiledlayout](create-custom-tiledlayout.md) - For animated dashboards
- [Customize Plot Appearance for Publication Quality](customize-plot-appearance.md) - For styling animations

## References

- [MATLAB Documentation: Animation Techniques](https://www.mathworks.com/help/matlab/animation-1.html)
- [MATLAB Documentation: drawnow](https://www.mathworks.com/help/matlab/ref/drawnow.html)
- [MATLAB Documentation: Improve Graphics Performance](https://www.mathworks.com/help/matlab/creating_plots/improve-graphics-update-performance.html)
- [MATLAB Documentation: VideoWriter](https://www.mathworks.com/help/matlab/ref/videowriter.html)
