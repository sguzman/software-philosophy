# Windows Dependency Policy

## Current convention

Ordinary CLI dependencies use Scoop.

Recommended declaration:

    Scoopfile.json

Recommended repo bootstrap:

    .\deps.ps1

The bootstrap may install/check Scoop, import the Scoopfile, verify language toolchains, and handle narrowly documented Windows-native workload exceptions.

## Language toolchains

Prefer their conventional committed declarations where appropriate, while keeping bootstrap/check repo-owned.

## Human QA

The director states whether dependencies need refresh, then the human invokes the repo-owned QA/build command.

Do not require downloaded CI/agent payloads for ordinary local QA.
