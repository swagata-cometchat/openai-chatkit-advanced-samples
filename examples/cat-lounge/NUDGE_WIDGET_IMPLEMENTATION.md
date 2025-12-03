# Nudge Cat Widget Implementation

## Overview
I've successfully implemented the nudge cat widget as requested. This interactive widget allows users to nudge or adore the cat through clickable buttons, providing a more engaging way to interact with the virtual cat.

## Components Implemented

### 1. Widget Template
- **File**: `/backend/app/widgets/cat_nudge.widget`
- **Description**: JSON widget template defining the Card layout with Image, Title, prompt text, and two interactive buttons (Nudge and Adore)

### 2. Widget Builder Function
- **File**: `/backend/app/widgets/profile_card_widget.py`
- **Function**: `build_nudge_cat_widget(state: CatState, prompt: str | None = None) -> WidgetRoot`
- **Description**: Builds the nudge widget using the cat's current state and an optional custom prompt

### 3. Cat State Methods
- **File**: `/backend/app/cat_state.py`
- **Methods**:
  - `nudge(boost: int = 1)`: Gently nudges the cat for a small happiness boost
  - `adore(boost: int = 3)`: Shows lots of love for a bigger happiness boost
- **Behavior**: Both actions increase happiness, with adore also providing a small energy boost

### 4. Server Action Handlers
- **File**: `/backend/app/server.py`
- **Methods**:
  - `_handle_nudge_action()`: Handles "cat.nudge" actions
  - `_handle_adore_action()`: Handles "cat.adore" actions
- **Behavior**: Both update cat state, add hidden context, and send response messages

### 5. Agent Tool
- **File**: `/backend/app/cat_agent.py`
- **Function**: `show_nudge_widget(prompt: str | None = None)`
- **Description**: Agent tool to display the interactive nudge widget
- **Updates**: Added to agent instructions and tool list with stop behavior

### 6. Frontend Integration
- **File**: `/frontend/src/components/ChatKitPanel.tsx`
- **Updates**: Added action handlers for "cat.nudge" and "cat.adore" actions
- **Behavior**: Sends server actions and updates cat state with visual feedback

## Usage

### For Users:
1. Ask the agent to show an interactive widget: *"Show me an interactive way to play with the cat"*
2. The agent will display the nudge widget with two buttons
3. Click **Nudge** for a gentle interaction (small happiness boost)
4. Click **Adore** for showing lots of love (bigger happiness and energy boost)

### For Agents:
- Call `show_nudge_widget()` when users want interactive cat features
- The widget includes actions that will be handled server-side
- Actions trigger state updates and appropriate responses

## Widget Actions

### cat.nudge
- **Effect**: +1 happiness, small chance for +1 energy
- **Response**: "You gently nudged {cat_name}! They seem a bit more alert now. *purr*"
- **Hidden Context**: `<CAT_NUDGED>{cat_name} was gently nudged</CAT_NUDGED>`

### cat.adore
- **Effect**: +3 happiness, +1 energy
- **Response**: "You showered {cat_name} with love! They're absolutely glowing with happiness! 😻"
- **Hidden Context**: `<CAT_ADORED>{cat_name} was showered with affection</CAT_ADORED>`

## Integration Notes

The implementation follows the existing patterns in the codebase:
- Uses the same widget template structure as other widgets
- Follows the action handling pattern established by the name suggestions widget
- Integrates with the existing cat state management system
- Provides appropriate feedback through flash messages and agent responses
- Includes hidden context for agent awareness of performed actions

The widget is now ready to be used alongside the existing quick actions in the cat status panel, providing users with an engaging way to interact with their virtual cat companion.