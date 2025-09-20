# Harmonizing function names and APIs
None

# Reorganizing/writing vignette
Editor suggestion to remove outdated language from vignette - https://github.com/ropensci/software-review/issues/620#issuecomment-1880183146
Search phrase: "consider removing 'new' so that this sentence is still valid many years from now"
```
# TODO: See
│   └── vignette_reword_diff.png
```

# Adding more useful material to a README
Reviewer suggestion to add statement of need - https://github.com/ropensci/software-review/issues/620#issuecomment-2033093650  
Search phrase: "Add statement of need. The `Who is Karel?` section of the README hints at the need but does not describe it explicitly"
```
# TODO: See examples/spanish/620_karel
readme_need_diff.png
```

# DRYing out code
Reviewer suggestion to reduce repeated test code using template approach - https://github.com/ropensci/software-review/issues/620#issuecomment-2033093650
Search phrase: "There is a lot of repeated code in `test-set_up.R` where each list of world elements (`world_test`) is being defined slightly differently. I think this could be simplified by starting with a single `world_test_template` list"
```
# TODO: See examples/spanish/620_karel
dry_template_diff.png
readme_need_diff.png
```

# Organizing functions into a more understandable set of files
None
