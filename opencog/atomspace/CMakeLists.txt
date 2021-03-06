#SET_DIRECTORY_PROPERTIES(PROPERTIES CLEAN_NO_CUSTOM true)

# The atom_types.h file is written to the build directory
INCLUDE_DIRECTORIES(${CMAKE_BINARY_DIR})

ADD_LIBRARY (atomspace
	AtomSpace.cc
	AtomSpaceInit.cc
	AtomTable.cc
	AttentionBank.cc
	BackingStore.cc
	FixedIntegerIndex.cc
	HandleSeqIndex.cc
	# HandleSetIndex.cc
	ImportanceIndex.cc
	# IncomingIndex.cc
	LinkIndex.cc
	NodeIndex.cc
	TLB.cc
	TypeIndex.cc
)

# Without this, parallel make will race and crap up the generated files.
ADD_DEPENDENCIES(atomspace opencog_atom_types)

TARGET_LINK_LIBRARIES(atomspace
	atombase
	truthvalue  
	lambda
	${COGUTIL_LIBRARY}
	${Boost_THREAD_LIBRARY}
)

INSTALL (TARGETS atomspace
	DESTINATION "lib${LIB_DIR_SUFFIX}/opencog"
)

INSTALL (FILES
	AtomSpace.h
	AtomTable.h
	AttentionBank.h
	BackingStore.h
	FixedIntegerIndex.h
	HandleSeqIndex.h
	ImportanceIndex.h
	LinkIndex.h
	NameIndex.h
	NodeIndex.h
	StringIndex.h
	TypeIndex.h
	TLB.h
	version.h
	DESTINATION "include/opencog/atomspace"
)
