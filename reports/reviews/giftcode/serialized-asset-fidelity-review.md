# Giftcode Serialized Asset Fidelity Review

Status: `Intentionally omitted from core scope; consumer integration required`.

## Source asset evidence

- `Assets/HUDs/GiftCode.ui` parses as structured JSON with root `_entityName`
  `GiftCode`, root ID `hXHZP3Iu`, two children (`DarkBG`, `Giftcode`), version
  `3`, and an attached `CustomUIUtils.fcg` reference.
- The UI contains `HUD_GIFTCODE_*` localization keys and requires source
  registration symbols `EResUIGiftCode`/`EResKeyGiftCode` verified in the source
  generated library and registration asset.
- `Assets/Sprites/Icons/GiftcodeIconTemp.png` and its metadata are source
  presentation assets.

## Decision

The user requested core logic, so the readable UI asset was not copied or
semantically edited. Preserving it byte-for-byte in SharedLibs would also import
source-specific `CustomUIUtils`, registration, localization, and menu bindings.
The asset is therefore classified as a consumer integration point, not a failed
core clone. Runtime UI fidelity still needs Studio verification when a consumer
chooses to add the feature.

