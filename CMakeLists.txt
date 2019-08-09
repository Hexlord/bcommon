
# file(GLOB SOE_SOMETHING_SRC
# 	"something/*.cpp"
# )

file(GLOB BCOMMON_SRC
	"../bgfx/examples/common/*.cpp"
	"../bgfx/examples/common/ps/*.cpp"
	"../bgfx/examples/common/nanovg/*.cpp"
	"../bgfx/examples/common/imgui/*.cpp"
	"../bgfx/examples/common/font/*.cpp"
	"../bgfx/examples/common/entry/*.cpp"
	"../bgfx/examples/common/debugdraw/*.cpp"
	"../bgfx/3rdparty/ib-compress/*.cpp"
	"../bgfx/3rdparty/ocornut-imgui/*.cpp"
)

if("${SOE_TARGET_OS}" STREQUAL "osx")
	set(OSX_ENTRY_CONDITIONAL "../bgfx/examples/common/entry/entry_osx.mm")
else()
	set(OSX_ENTRY_CONDITIONAL "")
endif()

file(GLOB BCOMMON_INC
	"../bgfx/examples/common/*.h"
	"../bgfx/examples/common/ps/*.h"
	"../bgfx/examples/common/ps/*.sc"
	"../bgfx/examples/common/nanovg/*.h"
	"../bgfx/examples/common/nanovg/*.sc"
	"../bgfx/examples/common/imgui/*.h"
	"../bgfx/examples/common/imgui/*.sc"
	"../bgfx/examples/common/font/*.h"
	"../bgfx/examples/common/font/*.sc"
	"../bgfx/examples/common/entry/*.h"
	"../bgfx/examples/common/entry/*.cx"
	"../bgfx/examples/common/debugdraw/*.h"
	"../bgfx/examples/common/debugdraw/*.sc"
	"../bgfx/3rdparty/ib-compress/*.h"
	"../bgfx/3rdparty/ocornut-imgui/*.h"
	"../bgfx/3rdparty/ocornut-imgui/*.inl"
	"../bgfx/3rdparty/ocornut-imgui/widgets/*.h"
	"../bgfx/3rdparty/ocornut-imgui/widgets/*.inl"
	"${OSX_ENTRY_CONDITIONAL}"
)

source_group(include FILES ${BCOMMON_INC})
source_group(src FILES ${BCOMMON_SRC})

include_directories( include )
include_directories( ../bx/include )
include_directories( ../bgfx/include )
include_directories( ../bgfx/3rdparty )
include_directories( ../bimg/include )

add_library(bcommon STATIC
	${BCOMMON_INC} ${BCOMMON_SRC} 
)

set_target_properties(bcommon PROPERTIES
	CLEAN_DIRECT_OUTPUT 1
)

target_link_libraries (bcommon bgfx bimg bx)

# file(COPY Data DESTINATION ..)