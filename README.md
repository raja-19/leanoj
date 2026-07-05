### current setup
- sqlite database
- /html/index.php handles html forms and serves web pages
- worker.php runs in the background and checks submissions:

  1. fetches next pending submission
  2. copies problem/answer and submission files into /checker-files
  3. compiles problem/answer and submission within /checker-files using lake
  4. tests submission declarations against problem/answer declarations using /checker scripts
  5. exports submission file using lean4export
  6. runs external typechecker (nanoda) on the export file
  7. updates submission status

steps 2 - 6 are run in a sandbox (isolate). because of that all (transitive) dependencies in /checker-files should be local. this is done by specifying local paths of dependencies in all lakefiles and updating lake-manifests.

### roadmap
1. organize (possibly rewrite) the codebase and properly deploy in a container
2. modernize the ui and add missing basic features (filtering, starring, etc.)
3. set up auto lean/mathlib update (including local dependencies setup in /checker-files)
4. figure out what to do next (e.g., lean guides for competitive math, molib)
5. write and integrate own external typechecker (not necessary but cool project)
