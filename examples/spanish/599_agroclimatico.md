# Harmonizing function names and APIs
Change function names to avoid confusion with existing packages - specifically changing `spi` to `spi_indice` and `spei` to `spei_indice` to avoid conflict with the SPEI package - https://github.com/ropensci/software-review/issues/599#issuecomment-1704935695
Search phrase: "podría plantearse un ligero cambio de nombre para evitar la confusión"

Consider changing function name `decil` to `cuantil` to better reflect what the function actually does - https://github.com/ropensci/software-review/issues/599#issuecomment-2273904912
Search phrase: "Ello me lleva a proponer un cambio de nombre de esta función"

# Reorganizing/writing vignette
None

# Adding more useful material to a README
Add more information about the package functionality and restructure README to show main functional blocks - https://github.com/ropensci/software-review/issues/599#issuecomment-1941871544
Search phrase: "tal vez se pueda añadir algo más o re-estructurar la información del README para que quede más claro, al menos en cuanto a los grandes bloques de funcionalidad del paquete"

Group functions in the reference index by thematic topics to make functionality clearer - https://github.com/ropensci/software-review/issues/599#issuecomment-1941871544
Search phrase: "Una sugerencia para que quede más clara la funcionalidad global del paquete es agrupar las funciones en el índice por temáticas"

Both reviewers suggested the README needs more information about package functionality - https://github.com/ropensci/software-review/issues/599#issuecomment-1941871544
Search phrase: "Ambas revisoras comentan que les gustaría ver más información sobre el paquete ahí"

# DRYing out code
Concern about repetitive functions in the ClimInd package - many functions for temperature calculations with different thresholds instead of one flexible function - https://github.com/ropensci/software-review/issues/599#issuecomment-1839892446
Search phrase: "las funciones son algo repetitivas (por ejemplo muchas funciones para calcular la temperatura mayor a distintos umbrales, en vez de 1 función que haga eso para cualquier umbral arbitrario)"

# Organizing functions into a more understandable set of files
None