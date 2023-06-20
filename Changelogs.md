
# 2023-06-20 
### Updated subheader_1.yaml and subheader_2.yaml to version 1.1
- Fix : no more cropped letters in contact with the corners of its container.

# 2023-06-21
### Updated climate.yaml to version 1.2
- Enhancement: now handles various hvac_modes. While version 1.1 was limited to the "heat" mode, the updated version should now manage multiple modes including "auto", "heat/cool", "heat", "cool", "fan", and "dry", and dynamically adjusts the card's color based on the selected mode.

### Updated fan.yaml to version 1.2
- Style : orange color has been replaced with blue color to better represent cooling, while keeping orange for heating entities.
- Enhancement: In addition to recognizing the "on" state, it now also recognizes any "fan" containing state.
