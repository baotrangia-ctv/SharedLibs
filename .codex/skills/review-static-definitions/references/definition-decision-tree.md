# Definition Decision Tree

Apply in order:

```text
Used only inside one function
    -> Keep local

Used only inside one Manager
    -> Keep private in Manager

Shared by Config and Manager
    -> Move to Config definitions under Assets/Scripts/Configs/

Shared by Manager and HUD
    -> Move to feature definitions under Assets/Scripts/Configs/

Shared by multiple modules
    -> Move to shared definitions
```

Group related field keys, states, result codes, and reused action identifiers in a small cohesive file such as `Assets/Scripts/Configs/MailsDefinitions.fcg`.

Split a definition file only when distinct ownership or size materially improves maintainability. Merge files that contain only one or a few tightly related constants.
