# AuraGuard Copilot Instructions

## Project Overview
AuraGuard is a critical home safety controller preventing dangerous fireplace gas back-drafting by controlling exhaust fans based on fireplace temperature and window status. This is a **safety-critical system** where incorrect logic could cause carbon monoxide poisoning.

## Key Safety Requirements
- If fireplace is running, window MUST be open (enforce this rule)
- If fireplace is cold (<36°C), fan can be turned ON or OFF regardless of window state
- Temperature threshold: 36°C is the critical boundary between "running" and "not running"

## Architecture & Hardware Integration
- **Target Hardware**: Shelly IoT devices (Gen4 Mini, Blu door/window sensor, Gen4 + Add-on for temperature)
- **Target Runtime**: Shelly scripts (JavaScript ES5 compatible)
- **Development Environment**: Node.js with mocked Shelly modules
- **API Reference**: https://shelly-api-docs.shelly.cloud/gen2/Scripts/Tutorial/

## Development Approach
- Use **devcontainer** for consistent development environment
- **Mock Shelly modules** for local development and testing
- Write **comprehensive unit tests** for all safety logic combinations
- ES5 compatibility required (no modern JS features like arrow functions, const/let)
- Follow Shelly Script API patterns for device communication

## Critical Code Patterns
When implementing fan control logic, always use this safety pattern:
```javascript
// Safety-first logic structure
if (temperature > 36 && windowOpen) {
    // Only case where fan can be ON
} else if (temperature > 36 && !windowOpen) {
    // DANGER: Force window open notification/action
} else {
    // Fan OFF for all other cases
}
```

## Testing Strategy
Test all state combinations:
- Hot fireplace + open window = fan allowed
- Hot fireplace + closed window = safety violation
- Cold fireplace + any window state = fan off
- Edge cases around 36°C temperature boundary

## Development Workflow
1. Set up devcontainer with Node.js and testing framework
2. Create Shelly module mocks matching official API
3. Implement safety logic with comprehensive tests
4. Validate ES5 compatibility before deployment
5. Test temperature sensor accuracy and window sensor reliability

## File Structure Expectations
- `/src/` - Main application logic
- `/tests/` - Unit tests for all safety scenarios  
- `/mocks/` - Shelly device mocks for development
- `/.devcontainer/` - Development container configuration
- `package.json` - Node.js dependencies and scripts