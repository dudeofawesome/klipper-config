# My custom Klipper macros

Check the macro's description for what it does and how to use it

### Some extended macro descriptions / help

- [`START_PRINT`](./print_start.cfg)

  - Slicer configuration

    - SuperSlicer

      `Printer Settings` → `Custom G-Code` → `Start G-Code`

      ```lisp
      ;Klipper start print macro
      START_PRINT HOTEND={first_layer_temperature[initial_extruder]+extruder_temperature_offset[initial_extruder]} BED={first_layer_bed_temperature} RELATIVE_E_MODE={use_relative_e_distances} PROBE=true PROBE_AREA_START={first_layer_print_min[0]},{first_layer_print_min[1]} PROBE_AREA_END={first_layer_print_max[0]},{first_layer_print_max[1]}
      ```

    - Cura

      **Note**: `PROBE_AREA_START` and `PROBE_AREA_END` rely on a non-official
      Cura plugin which I haven't tested.

      `Settings` → `Printers` → `Machine Settings` → `Start G-code`

      ```lisp
      ;Klipper start print macro
      START_PRINT HOTEND={material_print_temperature_layer_0} BED={material_bed_temperature_layer_0} RELATIVE_E_MODE={relative_extrusion} PROBE=false PROBE_AREA_START=%MINX%,%MINY% PROBE_AREA_END=%MAXX%,%MAXY%
      ```

- [`END_PRINT`](./print_end.cfg)

  - Slicer configuration

    - SuperSlicer

      `Printer Settings` → `Custom G-Code` → `End G-Code`

      ```lisp
      END_PRINT ;Klipper end print macro
      ```

    - Cura

      `Settings` → `Printers` → `Machine Settings` → `End G-code`

      ```lisp
      END_PRINT ;Klipper end print macro
      ```

- [`BEFORE_LAYER_CHANGE`](./layer_before_change.cfg)

  - Slicer configuration

    - SuperSlicer

      `Printer Settings` → `Custom G-Code` → `Before layer change G-Code`

      ```lisp
      BEFORE_LAYER_CHANGE
      ;{layer_z}
      ```

    - Cura

      `Extensions` → `Post Processing` → `Modify G-Code` → `Add a script` →
      `Insert at layer change`

      ```lisp
      BEFORE_LAYER_CHANGE
      ```

- [`SAFE_RETRACT`](./safe_retract.cfg)

  Safe retract relies on properly set firmware retraction values. As such, it
  can be helpful to set the values using a custom g-code command in your slicer

  - Slicer configuration

    - SuperSlicer

      `Filament Settings` → `Custom G-Code` → `Start G-Code`

      ```lisp
      ; Filament gcode
      SET_RETRACTION RETRACT_LENGTH={retract_length[current_extruder]} RETRACT_SPEED={retract_speed[current_extruder]} ;UNRETRACT_EXTRA_LENGTH={retract_length[current_extruder]} UNRETRACT_SPEED={retract_speed[current_extruder]}
      ```

- Pressure Advance

  This doesn't relate directly to a specific macro here, but it can also be
  useful to set your per-filament pressure advance values using custom g-code
  in your slicer as well

  - Slicer configuration

    - SuperSlicer

      `Filament Settings` → `Custom G-Code` → `Start G-Code`

      ```lisp
      ; Filament gcode
      SET_PRESSURE_ADVANCE ADVANCE=0.075 ; SMOOTH_TIME=pressure_advance_smooth_time
      ```
