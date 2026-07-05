- sqlite database used
- /html stores code that servers actual php pages
- worker.php runs as a background process:
  1. fetches next pending submission
  2. copies problem template/answer and submission into /checker-files
  3. compiles them in /checker-files
  4. checks that submission declarations match template/answer declarations using scripts defined in /checker
  5. exports submission using lean4export
  6. runs external checker (nanoda) on the export file
  7. updates submission status

steps 2 - 6 are run in a sandbox (isolate). this is why /checker-files has to use local packages. these are just normal packages (mathlib, etc.) with lakefiles modified to point to local versions of dependencies.
