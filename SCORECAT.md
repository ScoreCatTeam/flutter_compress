# ScoreCat fork of flutter_compress

This fork exists because ScoreCat's FlutterFlow app (`project-balance-rfs8cs`) installs it as a **git dependency pinned to a
commit** on the `scorecat/2.0.1-hdr` branch / `scorecat-2.0.1-hdr.N` tags. FlutterFlow builds fetch that commit on every export
and store build. **Do not delete this repository, make it private, or force-push/delete the `scorecat/*` branch or tags** —
any of those breaks every FlutterFlow build of the app.

Changes on top of upstream 2.0.1 (`446659d`), Android only (`android/src/main/kotlin/com/compress/all/flutter_compress/`):
1. Output video is always H.264 (`MimeTypes.VIDEO_H264`), and the export runs as a `Composition` with
   `HDR_MODE_TONE_MAP_HDR_TO_SDR_USING_OPEN_GL`. Upstream relies on Media3's default `KEEP_HDR`, which silently switches an
   H.264 request to HEVC-HDR on phones with an HEVC HDR encoder (e.g. Galaxy S26 10-bit HLG recordings).
2. `SizeMath` sizes on display axes (rotation-aware), so portrait clips get a 720-pixel short side.
3. The pre-cancel latch is re-checked after the job registers and before `transformer.start`.

Context: ScoreCatTeam/scorecat-app#463 (Android score-video uploads). Upstream: https://github.com/chenkaiHere/flutter_compress (MIT).
