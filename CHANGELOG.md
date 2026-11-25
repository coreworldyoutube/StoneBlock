# Changelog

## 0.3.0-dev — 2026-11-25

### Restored
- JSON resource registry with Japanese and English names.
- Coal and peat as generated fuel resources.
- Japanese/English UI translation data and language selector.
- World seed input, autosave, independent inventory save.
- Perlin geological regions, ore veins, cave pockets, exploration darkness, minimap.
- Native browser scrolling with a 10-block render buffer.
- Saved-data reset that clears world and inventory, then starts a new random-seed world at the center.

### Removed from this reconstruction
- Conveyor placement and transport simulation.
- Furnace placement and smelting simulation.
- Machine-specific save state and machine data registry.

### Compatibility
- Save format remains version 6. Older supported save versions remain accepted.
- Machine fields in older version-6 saves are ignored by this mining-only build.

### Validation status
- JavaScript syntax check: passed.
- Duplicate DOM IDs: none.
- Referenced DOM IDs: all found.
- Translation keys used by the interface: present in both language JSON files.
- Coal and peat generation branches: present.
- Browser/Android runtime behavior: not yet verified in a real browser/device.
