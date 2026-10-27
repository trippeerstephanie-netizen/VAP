# VAP WEST — release and data integrity checklist

This branch adds `west-end.html` and `west-end-map.html`. The second file is an exact Git blob clone of the original `index.html` at the time of branching; the citywide `index.html` remains untouched.

## Current behavior
- VAP WEST loads the cloned explorer with the same existing embedded property data.
- The selector focuses the map on nine West Louisville neighborhoods by approximate coordinates; it does **not** filter the underlying feature set by official neighborhood boundaries.
- Annual Cut List attribution: Neighborhood Improvement Committee (NIC) meeting, October 2026, firsthand attendee confirmation. The cut list is described as a foreclosure pipeline; it does not independently prove a filed lawsuit, completed foreclosure, or vacancy.
- A reset control restores the initial Louisville map view when the map instance is accessible.

## Release gate (do not merge until validated)
1. Obtain and verify official Louisville Metro neighborhood polygons for Russell, Shawnee, Portland, Chickasaw, Parkland, California, Park Hill, Algonquin, Taylor Berry.
2. Identify the actual feature layer objects in the cloned VAP HTML and classify their geometry/record identifiers. Apply a **spatial intersection** against the union of the nine official polygons to all relevant address-level layers, without changing source records.
3. Verify features on boundaries, null coordinates, non-point geometries, duplicates, and address search/export consistency. Display source and verification status.
4. Validate the map in a browser on desktop and mobile, test map focus and reset, keyboard controls, cross-origin assets, and console errors.
5. Confirm no private data, access tokens, or credentials are present in the published static HTML.
6. Update the VAP WEST page to display filtered counts and downloadable records **only after** validation.
7. Merge PR #1 and verify the published GitHub Pages URL.

Do not call the geographic focus an official neighborhood filter until steps 1–3 are completed. The existing VAP data can be accepted as the source dataset without inventing new records; spatial membership still requires testing.
