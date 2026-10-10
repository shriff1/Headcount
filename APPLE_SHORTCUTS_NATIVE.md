# Native Apple Shortcuts alternative — Headcount menu

You can build a **fully native Shortcut** that presents a menu and stores one persistent headcount in iCloud Drive. It does not require hosting a web app. It looks like an Apple Shortcuts menu, **not** the custom four-button screen in `index.html`.

A Shortcut generated outside Apple's app needs Apple signing before it can be imported on a modern iPhone. This document therefore lists the actions to create directly in Shortcuts; it is not a downloadable signed `.shortcut`.

## Action sequence

Create a new Shortcut called **Headcount**. In the Shortcuts editor, add the following actions in order. Use **Set Variable** to name the variables as shown; blue variable bubbles / Magic Variables should refer to the outputs of earlier actions.

1. **Get File from Folder**: choose the **Shortcuts** folder, enter path `headcount.txt`, and set **Error If Not Found** to **Off** (expand action details if necessary).
2. **If** the returned File **has any value**:
   - **Get Numbers from Input**: use the File variable as input.
   - **Set Variable** named `Count` to the extracted Number.
   - **Otherwise**:
   - **Number**: `0`.
   - **Set Variable** named `Count` to this Number.
   - **End If**.
3. **Number**: `0` → **Set Variable** named `Change` to this Number.
4. **Choose from Menu**. Add choices named **+1**, **−1**, **Add custom**, **Remove custom**, **See total**, and (optionally) **Reset**. Put these actions inside each corresponding menu branch:
   - **+1:** `Number 1` → `Set Variable Change` to `1`.
   - **−1:** `Number -1` → `Set Variable Change` to `-1`.
   - **Add custom:** `Ask for Input` (Input Type: **Number**, prompt “How many people arrived?”) → `Set Variable Change` to **Provided Input**.
   - **Remove custom:** `Ask for Input` (Input Type: **Number**, prompt “How many people left?”) → `Calculate` (**Provided Input × -1**) → `Set Variable Change` to **Calculation Result**.
   - **See total:** `Show Result` with `Current attendance: [Count]` → `Stop This Shortcut`.
   - **Reset:** `Number 0` → `Set Variable Count` to `0`. The **Change** variable remains `0` from step 3.
5. After **End Menu**, add **Calculate**: `[Count] + [Change]`. Then **Set Variable** named `UpdatedCount` to **Calculation Result**.
6. **If** `[UpdatedCount]` **is less than** `0`, add `Number 0` → `Set Variable UpdatedCount` to `0`, then **End If**. This prevents a negative attendance count.
7. **Text**: insert only the `[UpdatedCount]` variable into the Text field.
8. **Save File**: input the Text from step 7. Save in the **Shortcuts** folder with filename / path `headcount.txt`. Turn **Ask Where to Save** off, and **Overwrite If File Exists** on. The file is created on the first count update.
9. **Show Result**: `Total attendance: [UpdatedCount]`.

The menu closes after each change. Tap the Shortcut again for another adjustment. To place it on your Home Screen, open its details and tap **Add to Home Screen**.

### Notes

- The first use starts at zero. If **Get File from Folder** on your iOS version does not offer **Error If Not Found**, manually create `headcount.txt` in the `Shortcuts` folder containing `0`, using a temporary `Text(0)` → `Save File` shortcut.
- For simplicity, this native version saves only the running headcount. The web app adds arrival/exit totals, an undo button, and CSV export.
- When asking for a custom amount, enter a **positive whole number**; the native recipe does not independently validate that input. Removing more than the current count sets the result to zero.
- If Save File asks where to save, check the **Ask Where to Save** toggle and explicitly select the file as input.
