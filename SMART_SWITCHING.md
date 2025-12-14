# Smart Activity Switching

## Overview

AV Scenes intelligently handles activity transitions within the same room, minimizing device power cycling and reducing transition time.

## How It Works

### Traditional Activity Switching (OLD):
```
Current: "Watch TV" → New: "Watch Apple TV"

Steps:
1. Turn OFF all devices (Receiver, TV, Apple TV)
2. Wait for shutdown
3. Turn ON all devices for new activity
4. Wait for power-on delays
5. Set input sources

Result: ~20-30 seconds, visible interruption
```

### Smart Activity Switching (NEW):
```
Current: "Watch TV" → New: "Watch Apple TV"

Analysis:
- Receiver: In BOTH activities → KEEP ON
- TV: In BOTH activities → KEEP ON  
- Apple TV: In BOTH activities → KEEP ON
- Satellite Box: Only in old activity → TURN OFF

Steps:
1. Turn OFF Satellite Box (not needed)
2. Change Receiver input from "SAT" to "Apple TV"
3. Adjust volume if needed

Result: ~2-3 seconds, seamless transition
```

## Example Scenarios

### Scenario 1: TV → Apple TV
**"Watch TV" Activity:**
- Receiver (Input: SAT, Volume: 50%)
- TV (Input: HDMI1)
- Satellite Box

**"Watch Apple TV" Activity:**
- Receiver (Input: Apple TV, Volume: 60%)
- TV (Input: HDMI1)
- Apple TV

**Smart Switch Process:**
```
✓ Receiver stays ON → Input changes SAT → Apple TV, Volume 50% → 60%
✓ TV stays ON → No change needed
✗ Satellite Box → Turns OFF (not in new activity)
✓ Apple TV stays ON → Already on from previous use
```

**Time saved:** 15-20 seconds!

### Scenario 2: Movie → Gaming
**"Watch Movie" Activity:**
- Receiver (Input: BD/DVD, Volume: 65%)
- Projector (Input: HDMI1)
- Blu-ray Player

**"Gaming" Activity:**
- Receiver (Input: GAME, Volume: 70%)
- Projector (Input: HDMI1)
- PlayStation 5

**Smart Switch Process:**
```
✓ Receiver stays ON → Input changes BD/DVD → GAME, Volume 65% → 70%
✓ Projector stays ON → No change needed
✗ Blu-ray Player → Turns OFF
✓ PlayStation 5 → Turns ON (new device)
```

### Scenario 3: Music → Movie (Different devices)
**"Listen Music" Activity:**
- Receiver (Input: Bluetooth, Volume: 45%)

**"Watch Movie" Activity:**
- Receiver (Input: BD/DVD, Volume: 65%)
- Projector (Input: HDMI1)
- Blu-ray Player

**Smart Switch Process:**
```
✓ Receiver stays ON → Input changes Bluetooth → BD/DVD, Volume 45% → 65%
✓ Projector → Turns ON (new device, waits for power-on delay)
✓ Blu-ray Player → Turns ON (new device)
```

## Technical Details

### Device State Analysis

When switching activities, the coordinator:

1. **Identifies current devices:**
   ```python
   current_devices = {"receiver", "tv", "satellite"}
   ```

2. **Identifies new devices:**
   ```python
   new_devices = {"receiver", "tv", "apple_tv"}
   ```

3. **Calculates intersection (keep on):**
   ```python
   keep_on = current_devices & new_devices  # {"receiver", "tv"}
   ```

4. **Calculates difference (turn off):**
   ```python
   turn_off = current_devices - new_devices  # {"satellite"}
   ```

### Execution Order

**For devices to KEEP ON:**
```
1. Skip power-on command
2. Update input source (if changed)
3. Update volume (if changed)
```

**For devices to TURN OFF:**
```
1. Send turn_off command
2. No delay needed
```

**For devices to TURN ON:**
```
1. Send turn_on command
2. Wait for power-on delay
3. Set volume (if volume controller)
4. Set input source
```

## Configuration Best Practices

### Tip 1: Share Devices Across Activities

Design activities to share common devices:

**Good Example:**
```yaml
Living Room Activities:
  - Watch TV: [Receiver, TV, Satellite]
  - Watch Movie: [Receiver, TV, Blu-ray]
  - Gaming: [Receiver, TV, PlayStation]
  - Music: [Receiver]
```
→ Receiver and TV stay on for most switches

**Less Optimal:**
```yaml
Living Room Activities:
  - Watch TV: [TV, Satellite]
  - Watch Movie: [Projector, Blu-ray]
```
→ No shared devices, full restart needed

### Tip 2: Consistent Input Names

Use consistent device entity IDs across activities:
- ✓ `media_player.onkyo_receiver` in all activities
- ✗ Sometimes `media_player.receiver`, sometimes `media_player.onkyo`

### Tip 3: Volume Levels

Set appropriate volumes per activity:
- Music: Lower (40-50%)
- TV: Medium (50-60%)
- Movies: Higher (60-70%)
- Gaming: Highest (70-80%)

The volume automatically adjusts during smart switches!

## Logging

Enable debug logging to see smart switching in action:

```yaml
logger:
  logs:
    custom_components.av_scenes: debug
```

You'll see:
```
Smart switch: keeping 2 devices on, turning off 1 devices
Updating settings for already-on device: media_player.receiver
Changed input source to 'Apple TV' on media_player.receiver
Set volume to 60% on media_player.receiver
Turning off device: media_player.satellite
```

## Benefits

### User Experience
- ✓ Instant activity switching (2-3 seconds vs 20-30 seconds)
- ✓ No screen blackouts during transitions
- ✓ Seamless input source changes
- ✓ Natural workflow (like using a Harmony remote)

### Device Longevity
- ✓ Reduced power cycling extends device life
- ✓ Fewer relay clicks in receivers
- ✓ Less wear on projector lamps

### Energy Efficiency
- ✓ No unnecessary power-off/power-on cycles
- ✓ Devices stay at optimal operating temperature

## Edge Cases

### What if settings are identical?
If the device has the same input source and volume in both activities:
```
✓ Device stays on
✓ No commands sent
✓ Instant transition
```

### What if no devices overlap?
```
Old: [Device A, Device B]
New: [Device C, Device D]

Result: Full activity stop → start
(Same as before, smart switching can't help)
```

### What if volume controller changes?
```
Old Activity: Receiver is volume controller at 50%
New Activity: TV is volume controller at 60%

Result:
- Receiver: Volume stays at 50% (no longer controller)
- TV: Volume set to 60% (new controller)
```

## Comparison with Other Systems

### Logitech Harmony
Similar smart switching logic, but:
- AV Scenes: Open source, local control
- Harmony: Proprietary, cloud-dependent (discontinued)

### Manual Scenes
Traditional HA scenes:
- Always turn off → turn on
- No smart analysis
- Slower transitions

### Control4 / Crestron
Professional systems have similar logic:
- Much more expensive
- Requires programming
- AV Scenes brings this feature to DIY!

## Future Enhancements

Potential improvements:
- [ ] Configurable delay between activities
- [ ] Fade volume transitions
- [ ] Power state verification before switching
- [ ] Activity switch animations/notifications
- [ ] Multi-room synchronized switching

## Troubleshooting

**Issue:** Device doesn't change input source during switch  
**Solution:** Increase power-on delay, device might need more time to stabilize

**Issue:** Volume doesn't change during switch  
**Solution:** Verify volume controller is marked correctly in both activities

**Issue:** Device turns off unexpectedly  
**Solution:** Check that device entity_id is identical in both activities (case-sensitive!)
