# Input Data Persistence Fix - localStorage Implementation

## Problem
When users switched between tabs/pages in the PHWEB system, all input values (text, dates, selects) were disappearing because they only existed in the browser's memory for that specific page.

## Solution
Implemented **localStorage** to persist form data across page navigation. Each page now automatically saves user input to the browser's local storage and restores it when the page is revisited.

## Changes Made

### Files Modified
1. **purchase_request.html** - Added localStorage for purchase request form
2. **request_for_qoutation.html** - Added localStorage for quotation form
3. **philgeps_posting.html** - Added localStorage for PHILGEPS posting form
4. **notice_of_award.html** - Added localStorage for NOA form
5. **contract.html** - Added localStorage for contract form

### Implementation Details

#### New Functions Added to Each File

1. **`saveToLocalStorage()`**
   - Called whenever user input changes (on blur/change events)
   - Saves all row data (inputs and selects) as JSON to localStorage
   - Uses unique storage keys per page (e.g., "purchase_request_data")

2. **`loadFromLocalStorage()`**
   - Runs when page loads via DOMContentLoaded event
   - Retrieves saved data from localStorage
   - Reconstructs all rows with their previous values

3. **`attachInputListeners()`**
   - Attaches change and blur event listeners to all inputs and selects
   - Ensures every user modification is saved automatically

#### Automatic Triggers for Saving Data
- Input/select value changes
- Blur events (when user leaves a field)
- Adding new rows (+ button)
- Undo/Redo operations (Ctrl+Z)
- Copy/Paste operations (Ctrl+C / Ctrl+V)

#### Storage Keys Per Page
- `purchase_request_data` → purchase_request.html
- `request_for_quotation_data` → request_for_qoutation.html
- `philgeps_posting_data` → philgeps_posting.html
- `notice_of_award_data` → notice_of_award.html
- `contract_data` → contract.html

## How It Works

1. **On Page Load**: 
   - Page checks localStorage for previously saved data
   - If data exists, it restores all rows and values

2. **During User Input**:
   - Every change is automatically saved to localStorage
   - No manual "save" button needed

3. **On Tab Switch**:
   - When user navigates to another page, data is preserved in localStorage
   - When user returns to previous page, data is automatically restored

## Browser Compatibility
- Works on all modern browsers (Chrome, Firefox, Safari, Edge)
- Each browser profile maintains separate localStorage
- Data persists until browser cache is cleared or user clears site data

## Important Notes
- localStorage data is **NOT** cleared when browser closes (persists until manually cleared)
- Users can clear their browser data to reset all forms if needed
- Data is stored locally only, not sent to any server
- Each browser/device/profile maintains separate storage

## Testing
To verify the fix works:
1. Fill in data on any form (purchase request, quotation, etc.)
2. Navigate to another tab/page
3. Return to the previous page
4. All your data should be restored automatically
