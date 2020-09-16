## Note on automation

Often you want to add build support to run simulations automatically. One way to do this is with CMake as the following example shows:

```
cmake_minimum_required(VERSION 3.15)

project(flow LANGUAGES )

set(CIRCUIT "src.ckt" CACHE STRING "Circuit")
set(PLOTSCRIPT "plot_tr.p" CACHE STRING "Plot script")

# https://cliutils.gitlab.io/modern-cmake/chapters/basics/variables.html
message(STATUS "Circuit: ${CIRCUIT}")

add_custom_target(sim COMMAND gnucap -b ${CIRCUIT})

add_custom_Target(plot COMMAND gnuplot ${PLOTSCRIPT})
```


