# Repository structure

One app, one backplane, one agent contract.

```
.
  docs/                 product contract, ADRs, grill plans
  .agents/              single root contract, including plans/
  Api/
    AppHost/            Aspire host for local backplane
    Services/Relay/     backplane
    Libraries/Rig.Data/ EF model
    Tests/
  Apps/
    rig/                the Flutter shell
    shared/             Flutter libraries
  deploy/               compose, vault profile off by default
```

No nested `.agents/` under `Api/` or `Apps/`.
