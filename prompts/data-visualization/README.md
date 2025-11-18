# Data Visualization

Prompts for creating visualizations in MATLAB with custom styling, animations, and optimized graphics.

## Prompts in this Category

### [Create Custom Multi-Panel Visualizations with Tiledlayout](create-custom-tiledlayout.md)
Design publication-quality multi-panel figures using tiledlayout with optimized performance. Perfect for dashboards, comparison plots, and complex layouts.

**Tags:** `matlab` `visualization` `tiledlayout` `plotting` `performance` `graphics`
**Release:** R2019b+

### [Create High-Performance Animated Plots](create-animated-plots.md)
Create smooth animations by updating plot data efficiently without recreating graphics objects. Includes patterns for real-time data visualization and saving animations.

**Tags:** `matlab` `visualization` `animation` `performance` `drawnow` `graphics`
**Release:** All releases

### [Customize Plot Appearance for Publication Quality](customize-plot-appearance.md)
Transform basic MATLAB plots into publication-ready figures with custom colors, fonts, line styles, and professional styling.

**Tags:** `matlab` `visualization` `styling` `publication` `graphics` `customization`
**Release:** All releases

### [Convert Multiple Plots to Tiled Layout](convert-plots-to-tiledlayout.md)
Transform separate figure windows or subplots into a modern tiled layout using tiledlayout and nexttile. Perfect for creating publication-ready multi-panel figures with consistent formatting.

**Tags:** `matlab` `visualization` `plotting` `layout` `graphics` `tiledlayout`
**Release:** R2019b+ (tiledlayout introduced)

## Performance Guidelines

All prompts in this category follow MATLAB graphics performance best practices:

- **Update, don't recreate:** Modify XData/YData properties instead of recreating plot objects
- **Modern syntax:** Use dot notation and tiledlayout for better performance
- **Manual limits:** Set axis limits explicitly to prevent auto-calculation overhead
- **Efficient rendering:** Use drawnow limitrate for animations
- **Object consolidation:** Combine data into single objects when possible

## Related Categories

- [App Building](../app-building/) - For building interactive visualization apps
- [Image Processing and Computer Vision](../image-processing-and-computer-vision/) - For image display and analysis
- [Live Scripts & Documentation](../live-scripts-documentation/) - For interactive documents with embedded graphics
- [Signal Processing](../signal-processing/) - For signal visualization and spectral analysis

## Contributing

Have a prompt for MATLAB data visualization? See [CONTRIBUTING.md](../../CONTRIBUTING.md) for guidelines.
