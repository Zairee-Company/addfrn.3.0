# Tap/Click to Open Player Profile

## ✅ Feature Overview

When you **tap or click** on any player in the game, their avatar profile will automatically open with all buttons available!

## 🎮 How It Works

### Desktop (Mouse Click)
- **Left-click** on any player's character
- Profile opens immediately

### Mobile/Tablet (Touch)
- **Tap** on any player's character
- Profile opens immediately

### Cooldown Protection
- 0.6 second cooldown between opening profiles
- Prevents accidental multiple opens

## 📋 What Appears in the Profile

When you tap/click a player, the profile shows:

1. **Avatar Image** - Player's headshot thumbnail
2. **Player Name** - "Target: [PlayerName]"
3. **Bio/Status** - "Status: Player since X days"
4. **Buttons:**
   - **Sync** - Sync with player (calls Sync RemoteEvent)
   - **Unsync** - Unsync from player (calls Unsync RemoteEvent)
   - **Add Friend** - Send friend/connection request
   - **View** - View player (placeholder for custom action)
5. **Close Button** - X button in header to close

## 🔧 Technical Details

### Detection System
- **Mouse**: Uses `mouse.Button1Down` event
- **Touch**: Uses `UserInputService.TouchStarted` with raycast
- **Raycast**: 2000 stud range, filters out your own character

### Profile Opening
- Calls `openProfileFor(targetPlayer)`
- Sets `_G.CurrentProfilePlayer` for friend request system
- Updates button states (e.g., "Friends ✓" if already friends)
- Shows visual highlight on player character

### Code Location
**File**: `StarterPlayer/StarterPlayerScripts/AvatarProfileAllInOne.lua`
- Lines 365-379: `playerFromPart()` - Detects player from clicked part
- Lines 384-391: `tryOpenPlayer()` - Opens profile with cooldown
- Lines 393-399: Mouse click handler
- Lines 401-413: Touch input handler
- Lines 167-195: `openProfileFor()` - Opens and populates profile

## 🎨 Visual Effects

When profile opens:
- **Highlight Effect**: Blue pulsing outline around target player (1.4 seconds)
- **Smooth Animation**: Profile frame appears
- **Avatar Loading**: Player thumbnail loads asynchronously

## ⚙️ Requirements

For tap-to-open to work, you need:

1. **AvatarProfileGui** in StarterGui with structure:
   ```
   AvatarProfileGui (ScreenGui)
   └── ProfileFrame (Frame)
       ├── Header
       │   └── Close (TextButton)
       ├── Content
       │   ├── AvatarImage (ImageLabel)
       │   └── RightCol (Frame)
       │       ├── TargetName (TextLabel)
       │       └── Bio (TextLabel)
       └── Buttons (Frame)
           ├── Sync (TextButton)
           ├── Unsync (TextButton)
           ├── Add Friend (TextButton)
           └── View (TextButton)
   ```

2. **Script Location**: `AvatarProfileAllInOne.lua` in `StarterPlayer/StarterPlayerScripts/`

## 🐛 Troubleshooting

**Profile not opening when tapping?**
- Check that `AvatarProfileGui` exists in StarterGui
- Verify script is in `StarterPlayer/StarterPlayerScripts/`
- Check Output window for errors
- Make sure you're clicking/tapping on the player's character (not empty space)

**Buttons not showing?**
- Verify all buttons exist in `ProfileFrame/Buttons/`
- Check button names match exactly: "Sync", "Unsync", "Add Friend", "View"
- Check Output for warnings about missing buttons

**Touch not working on mobile?**
- Ensure `UserInputService` is available (should be automatic)
- Check that touch input isn't being processed by other GUIs
- Verify raycast isn't hitting invisible parts

## 🎯 Button Functions

### Sync Button
- Closes profile
- Calls `ReplicatedStorage.Sync` RemoteEvent
- Shows highlight effect

### Unsync Button
- Closes profile
- Calls `ReplicatedStorage.Unsync` RemoteEvent
- Shows highlight effect

### Add Friend Button
- Sends in-game connection request
- Sends real Roblox friend request
- Updates button text to "Request Sent!"
- Closes profile after 2 seconds

### View Button
- Currently prints to Output (placeholder)
- You can customize this for your needs

### Close Button
- Closes profile
- Clears current target

## ✨ Customization

To customize the View button action, edit line 352-356 in `AvatarProfileAllInOne.lua`:

```lua
if viewBtn and viewBtn:IsA("GuiButton") then
	viewBtn.MouseButton1Click:Connect(function()
		if not currentTarget then return end
		-- Add your custom action here
		-- Example: Open player's profile page, teleport to player, etc.
	end)
end
```

---

**The tap-to-open profile feature is fully functional!** Just tap any player to see their profile! 🎉

