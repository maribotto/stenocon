# Stenocon Selection Logic Pseudocode

## State

```
activeElement  = null     // Active stenocon element
lmbDown        = false    // Is LMB held down
rmbDown        = false    // Is RMB held down
firstButton    = null     // Which was pressed first: 'lmb' | 'rmb' | null
selectionMade  = false    // Has a selection been made (blocks new selections)
swapped        = false    // Modifier (Shift) or page switch (Tab) active
```


## handleMouseDown(e)

```
IF selectionMade == true:
    RETURN (requires full release before new selection)

activeElement = clicked element

IF e.button == LMB AND lmbDown == false:
    lmbDown = true
    IF firstButton == null:
        firstButton = 'lmb'

IF e.button == RMB AND rmbDown == false:
    rmbDown = true
    IF firstButton == null:
        firstButton = 'rmb'

update visuals
```


## handleMouseUp(e)

```
IF activeElement == null OR selectionMade == true:
    update released button state (lmbDown/rmbDown = false)
    IF both released:
        resetState()
    RETURN

swapped = modifierActive OR pageSwitch

IF e.button == LMB (LMB was released):

    IF lmbDown AND rmbDown AND firstButton == 'rmb':
        // RMB first, LMB second, LMB released = RL selection
        selection = swapped ? 'R' : 'RL'
        make selection
        selectionMade = true

    ELSE IF lmbDown AND NOT rmbDown AND firstButton == 'lmb':
        // Only LMB was pressed and released = L selection
        selection = swapped ? 'LR' : 'L'
        make selection
        selectionMade = true

    // ELSE: LMB released but RMB was first and still held = cancel

    lmbDown = false

IF e.button == RMB (RMB was released):

    IF lmbDown AND rmbDown AND firstButton == 'lmb':
        // LMB first, RMB second, RMB released = LR selection
        selection = swapped ? 'L' : 'LR'
        make selection
        selectionMade = true

    ELSE IF rmbDown AND NOT lmbDown AND firstButton == 'rmb':
        // Only RMB was pressed and released = R selection
        selection = swapped ? 'RL' : 'R'
        make selection
        selectionMade = true

    // ELSE: RMB released but LMB was first and still held = cancel

    rmbDown = false

update visuals

IF NOT lmbDown AND NOT rmbDown:
    resetState()  // Full reset when both buttons released
```


## Selection Logic Summary

| Action                            | Result (normal) | Result (swapped) |
|-----------------------------------|-----------------|------------------|
| LMB click                         | L               | LR               |
| RMB click                         | R               | RL               |
| LMB down → RMB down → RMB up      | LR              | L                |
| RMB down → LMB down → LMB up      | RL              | R                |
| LMB down → RMB down → LMB up      | cancel          | cancel           |
| RMB down → LMB down → RMB up      | cancel          | cancel           |


## Cancellation Logic

Selection is cancelled if buttons are released in the "wrong" order:
- If the first button is released before the second (when both are held)
- Selection only occurs when the **second** button is released
