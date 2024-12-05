# Oil Price Widget
![image](https://github.com/user-attachments/assets/6fc0e44e-f0f0-4815-a4c0-a292dc1b6521)

A lightweight, embeddable widget that displays real-time oil prices using the OilPriceAPI service.

![Oil Price Widget Preview](widget-preview.png)

## Features

- Real-time oil price updates
- Clean, modern design with system font
- Automatic price refresh every 5 minutes
- Responsive layout with shadow effects
- Last update timestamp display
- Error handling for failed API calls

## Installation

Simply copy and paste the following code snippet into your HTML file:

```html
<script>
    !function() {
        let container = document.createElement("div");
        container.innerHTML = `
            <div style="font-family: system-ui; border: 1px solid #ddd; padding: 15px; border-radius: 8px; max-width: 300px; box-shadow: 0 2px 4px rgba(0,0,0,0.1)">
                <h3 style="margin: 0; color: #333;">Live Oil Price</h3>
                <div id="oilprice" style="font-size: 28px; font-weight: bold; margin: 10px 0;">Loading...</div>
                <div id="oiltime" style="font-size: 12px; color: #666;"></div>
                <div style="font-size: 11px; margin-top: 10px; text-align: right;">via <a href="https://api.oilpriceapi.com" style="color: #007bff; text-decoration: none;">OilPriceAPI</a></div>
            </div>
        `;
        document.body.appendChild(container);
        const fetchPrice = async () => {
            try {
                const response = await fetch('https://api.oilpriceapi.com/prices');
                const data = await response.json();
                document.getElementById("oilprice").textContent = data.formatted;
                document.getElementById("oiltime").textContent = `Updated: ${new Date(data.created_at).toLocaleString()}`;
            } catch (error) {
                document.getElementById("oilprice").textContent = "Error loading price";
                console.error("Error:", error);
            }
        };
        fetchPrice();
        setInterval(fetchPrice, 300000); // Update every 5 minutes
    }();
</script>
```

## Configuration

The widget is self-contained and requires no additional configuration. However, you may want to customize:

- Update interval (default: 300000ms / 5 minutes)
- Widget styling (fonts, colors, dimensions)
- Error messages

## API Requirements

This widget requires an API key from [OilPriceAPI](https://api.oilpriceapi.com). Sign up for an account to obtain your API key.

## Customization

To modify the widget's appearance, adjust the inline styles in the `container.innerHTML` section. The widget uses:

- system-ui font family for modern look
- Subtle border and shadow for depth
- Responsive max-width of 300px
- 8px border radius for rounded corners

## Browser Support

The widget supports all modern browsers including:
- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## License

MIT License - feel free to modify and use this widget in your projects.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
