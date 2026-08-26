# GitHub Upload Steps

## Before public release

1. Replace author placeholders in `CITATION.cff`.
2. Add exact PlanetScope acquisition metadata.
3. Add OSM extraction/download date and source.
4. Document the river/sandbar mask source and delineation procedure.
5. Confirm that no licensed PlanetScope raster, local geodatabase, or private data were copied into the repository.
6. Run `python tools/validate_repository.py`.
7. If the original final environment still exists, run `pip freeze > requirements-lock.txt` and review the file before committing.

## Recommended repository name

`rajshahi-urban-expansion-planetscope`

## GitHub website

1. Create a new repository with the name above.
2. Do not add a second README during creation.
3. Extract the provided ZIP.
4. Upload the **contents** of the `rajshahi-urban-expansion-planetscope` folder.
5. Commit with: `Initial reproducible analysis release`.

## Git commands (optional)

```bash
git init
git add .
git commit -m "Initial reproducible analysis release"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/rajshahi-urban-expansion-planetscope.git
git push -u origin main
```

Do not upload raw PlanetScope imagery unless your license explicitly permits redistribution, `.venv`, large temporary rasters, credentials, or personal absolute paths.
