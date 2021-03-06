#-----------------------------------------------------------------------------
#
#  CMake Config
#
#  Osmium Tool Tests - extract
#
#-----------------------------------------------------------------------------

function(check_extract _name _input _output _opts)
    check_output(extract ${_name} "extract --generator=test -f osm extract/${_input} ${_opts} -b 0,0,1.5,10" "extract/${_output}")
endfunction()

function(check_extract_cfg _name _input _output _opts)
    check_output(extract cfg_${_name} "extract --generator=test extract/${_input} ${_opts} -c ${CMAKE_CURRENT_SOURCE_DIR}/config.json" "extract/${_output}")
endfunction()


#-----------------------------------------------------------------------------

check_extract(simple        input1.osm output-simple.osm "-s simple --output-header=xml_josm_upload!")
check_extract(complete_ways input1.osm output-complete-ways.osm "-s complete_ways")
check_extract(smart_default input1.osm output-smart.osm "-s smart")
check_extract(smart_mp      input1.osm output-smart.osm "-s smart -S types=multipolygon")
check_extract(smart_any     input1.osm output-smart.osm "-s smart -S types=any")
check_extract(smart_nonmp   input1.osm output-smart-nonmp.osm "-s smart -S types=x")

check_extract_cfg(simple    input1.osm output-simple.osm "-s simple --output-header=xml_josm_upload=false")


#-----------------------------------------------------------------------------
