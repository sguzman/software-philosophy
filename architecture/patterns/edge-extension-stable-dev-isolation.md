# Edge Extension Stable / Dev Isolation

Modality: **PATTERN / PLATFORM-SPECIFIC CURRENT CONVENTION**

Applies when an Edge extension has become load-bearing while development must continue.

Derived from the `edge-tts` recovery and isolation design.

## Canonical layout

For unpacked Edge extensions that execute directly from repository files, prefer:

    NORMAL EDGE PROFILE
      stable extension
      stable worktree/path
      verified consumption runtime

    DEVELOPMENT EDGE PROFILE
      dev extension
      development worktree/path
      experimental QA runtime

The stable and development copies remain one project lineage but use different filesystem paths and different Edge profiles.

## Why separate Edge profiles

Different extension filesystem paths normally produce distinct unpacked-extension identities when manifests do not force the same key, which separates extension storage, service-worker lifecycle, reload/uninstall actions, and related extension-scoped state.

A separate Edge profile adds a second operational boundary:
- stable browsing/reading happens in the normal profile;
- dev QA happens in a laboratory profile;
- accidental invocation of the wrong extension is less likely;
- a broken dev tab/window can be abandoned without disturbing the normal profile.

For a load-bearing extension, this is preferred over installing stable and dev side by side in one everyday profile even if the extension IDs differ.

## Same-document collision audit

Distinct extension identities do **not** guarantee same-page safety.

Audit whether stable and dev content scripts share:
- DOM IDs;
- CSS classes;
- data attributes;
- Custom Highlight names;
- global event names;
- injected style IDs;
- cleanup selectors;
- page-level singleton markers.

A development bootstrap that searches for generic production UI selectors and removes them can destroy the stable page session even though the browser sees two distinct extensions.

Until page-level identifiers are channel-namespaced or otherwise collision-safe, do not intentionally activate stable and dev on the same document.

## Audio / speech ownership

Two extension identities may still share browser-global or device-global speech/audio resources.

Audit:
- Web Speech / speechSynthesis cancellation semantics;
- direct audio playback overlap;
- audio ownership bookkeeping;
- global stop/cancel calls;
- media-session integration if present.

Do not assume each extension knows the other owns audio.

If concurrent speech has not been designed and tested, manual QA should avoid simultaneous stable/dev playback.

## Native Messaging

Native Messaging is external OS state and must be included in the channel-isolation design.

Prefer distinct host identities and install locations, for example:

    com.example.product.feature
      -> stable host manifest/executable

    com.example.product.feature.dev
      -> development host manifest/executable

Each host should authorize only the intended extension identity/origin as appropriate.

Dev install/update/uninstall must not overwrite or remove the stable host registration.

A single global host manifest whose `allowed_origins` is rewritten between stable and dev is not an isolated dual-channel design.

## Shared system adapters

Some native adapters may be intentionally system-wide.

Do not automatically duplicate or unregister them if:
- they are genuinely shared infrastructure;
- coexistence has been verified;
- stable does not depend on dev-specific mutation of them.

Classify them as **GLOBAL BUT ACCEPTABLE** or another explicit collision-audit status rather than pretending they are isolated.

Dev uninstall must not unregister shared infrastructure still required by stable.

## Reload discipline

Reloading the dev extension should affect only the dev Edge profile/extension identity.

Reloading stable should be rare and should normally occur only after an accepted stable promotion or deliberate recovery action.

Existing tabs may retain old content-script state after extension reload. Manual QA should account for page refresh/reinjection semantics rather than assuming extension reload alone proves the new code is active.

## Promotion rule

A dev commit should advance stable only after the exact candidate is exercised in real Edge against the continuity envelope.

For a TTS/reader-like extension, likely gates include:
- extension starts normally;
- primary reading/play path works;
- stop/quit works;
- highlighting/UI lifecycle works;
- existing relied-upon voice/backend still works;
- changed/new backend is exercised if relevant;
- stable/dev isolation hazards introduced by the change are reviewed;
- the principal explicitly accepts the candidate when experiential QA is required.

Automated tests and native-helper tests remain evidence, but they are not substitutes for visible browser runtime evidence.

## Operational recovery invariant

The target recovery action after a dev catastrophe is:

    close/leave dev Edge profile
      -> return to normal stable Edge profile
      -> continue using the extension

No branch switch, uninstall, reset, stable repair, or settings reconstruction should be required.

## Schema for future Edge extension projects

When an Edge extension becomes load-bearing, record:

1. stable branch/version and filesystem path;
2. dev branch and filesystem path;
3. stable Edge profile;
4. dev Edge profile;
5. extension identity assumptions (`key`, path-derived ID, etc.);
6. page/DOM/CSS namespace collision audit;
7. extension storage/service-worker isolation;
8. audio/device ownership collision audit;
9. Native Messaging host/channel separation;
10. shared system registrations/adapters;
11. uninstall/reset blast radius;
12. exact stable-promotion QA gates.

## Governing guarantee

> **A dev extension failure may cost the laboratory tab/profile; it must not cost the principal the working stable extension.**
