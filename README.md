# AuraGuard

## Overview

AuraGuard is a critical home safety controller that prevents the dangerous back-drafting of fireplace gases by exhaust fans. It ensures the fan operates only when the fireplace is active (hot) and a window is open to provide necessary makeup air.

## Hardware Components

- **Fan Controller**: [Shelly 1 Mini Gen4](https://www.shelly.com/de/products/shelly-1-mini-gen4)
- **Window Sensor**: [Shelly Blu Door/Window Sensor](https://www.shelly.com/de/products/shelly-blu-door-window-white)
- **Temperature Monitoring**: [Shelly 1 Gen4](https://www.shelly.com/de/products/shelly-1-gen4) with [Shelly Plus Add-on](https://www.shelly.com/de/products/shelly-plus-add-on)

## Safety Requirements

### Core Logic
- **Fan can be turned on when window is open**
- **If the fireplace is running, the window has to be opened**
- **If the fireplace is not running, the window does not need to be opened**

### Temperature Thresholds
- **Fireplace running**: Temperature > 36°C
- **Fireplace not running**: Temperature ≤ 36°C

### Control Methods
- Fan can be turned on via Shelly App
- Fan can be turned on via connected switch (SW Port → Input:0)

## Development

For implementation details, development setup, and coding guidelines, see [`.github/copilot-instructions.md`](.github/copilot-instructions.md).