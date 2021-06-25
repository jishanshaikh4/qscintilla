CMAKE_MINIMUM_REQUIRED(VERSION 3.0.0)
CMAKE_POLICY(SET CMP0048 OLD)
PROJECT(qscintilla2)
SET(CMAKE_CXX_STANDARD 11)

FUNCTION(INSTALL_FILES_HIERARCHY)
  SET(options OPTIONAL)
  SET(multiValueArgs FILES)
  SET(oneValueArgs DESTINATION)

  CMAKE_PARSE_ARGUMENTS(INSTALL_FILES_HIERARCHY "${options}" "${oneValueArgs}" "${multiValueArgs}" ${ARGN})
  FOREACH(file ${INSTALL_FILES_HIERARCHY_FILES})
    GET_FILENAME_COMPONENT(dir ${file} DIRECTORY)
    INSTALL(FILES ${file} DESTINATION ${INSTALL_FILES_HIERARCHY_DESTINATION}/${dir})
  ENDFOREACH()
ENDFUNCTION()

SET(CMAKE_AUTOMOC ON)
FIND_PACKAGE(Qt5 COMPONENTS Core Gui Widgets LinguistTools)
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${Qt5Core_EXECUTABLE_COMPILE_FLAGS} ${Qt5Gui_EXECUTABLE_COMPILE_FLAGS} ${Qt5Widgets_EXECUTABLE_COMPILE_FLAGS}")
IF(Qt5_POSITION_INDEPENDENT_CODE)
  SET(CMAKE_POSITION_INDEPENDENT_CODE ON)
ENDIF(Qt5_POSITION_INDEPENDENT_CODE)
IF(CMAKE_SYSTEM_NAME MATCHES "Darwin")
  FIND_PACKAGE(Qt5 COMPONENTS MacExtras)
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${Qt5MacExtras_EXECUTABLE_COMPILE_FLAGS}")
ENDIF()
  
INCLUDE_DIRECTORIES(. ../include ../lexlib ../src)
ADD_DEFINITIONS(-DSCINTILLA_QT -DSCI_LEXER -DFASTO)

# If the user did not customize the install prefix,
# set it to live under build so we don't inadvertently pollute /usr/local
IF(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  SET(CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}/install" CACHE PATH "default install path" FORCE)
ENDIF(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)

SET(HEADER_INCLUDE
  Qsci/qsciscintilla.h
  Qsci/qsciscintillabase.h
  Qsci/qsciabstractapis.h
  Qsci/qsciapis.h
  Qsci/qscilexer.h
  Qsci/qscilexercustom.h
  Qsci/qsciglobal.h
  Qsci/qscicommand.h
  Qsci/qscidocument.h
  Qsci/qscilexerjson.h
  Qsci/qscilexerxml.h
  Qsci/qscilexerhtml.h
  Qsci/qscilexerpython.h
  Qsci/qscilexerjavascript.h
  Qsci/qscilexercpp.h
)

SET(HEADERS
    #Qsci/qscilexerbash.h
    #Qsci/qscilexerbatch.h
    #Qsci/qscilexercmake.h
    #Qsci/qscilexercpp.h
    #Qsci/qscilexercsharp.h
    #Qsci/qscilexercss.h
    #Qsci/qscilexerd.h
    #Qsci/qscilexerdiff.h
    #Qsci/qscilexerfortran.h
    #Qsci/qscilexerfortran77.h
    #Qsci/qscilexeridl.h
    #Qsci/qscilexerjava.h
    #Qsci/qscilexerjavascript.h
    #Qsci/qscilexerlua.h
    #Qsci/qscilexermakefile.h
    #Qsci/qscilexermatlab.h
    #Qsci/qscilexeroctave.h
    #Qsci/qscilexerpascal.h
    #Qsci/qscilexerperl.h
    #Qsci/qscilexerpostscript.h
    #Qsci/qscilexerpov.h
    #Qsci/qscilexerproperties.h
    #Qsci/qscilexerpython.h
    #Qsci/qscilexerruby.h
    #Qsci/qscilexerspice.h
    #Qsci/qscilexersql.h
    #Qsci/qscilexertcl.h
    #Qsci/qscilexertex.h
    #Qsci/qscilexerverilog.h
    #Qsci/qscilexervhdl.h
    #Qsci/qscilexerxml.h
    #Qsci/qscilexerhtml.h
    #Qsci/qscilexeryaml.h
    #Qsci/qscimacro.h
    SciClasses.h
    SciAccessibility.h
    ScintillaQt.h
    ../src/XPM.h
    Qsci/qsciglobal.h
    Qsci/qscicommand.h
    Qsci/qscicommandset.h
    Qsci/qscidocument.h
    Qsci/qsciprinter.h
    Qsci/qscistyle.h
    ../src/ViewStyle.h
    Qsci/qscistyledtext.h
    ListBoxQt.h
    SciNamespace.h    
    ../include/ILexer.h
    ../include/Platform.h
    ../include/SciLexer.h
    ../include/Scintilla.h
    ../include/ScintillaWidget.h
    ../src/UniConversion.h
    ../lexlib/Accessor.h
    ../lexlib/CharacterCategory.h
    ../lexlib/CharacterSet.h
    ../lexlib/LexAccessor.h
    ../lexlib/LexerBase.h
    ../lexlib/LexerModule.h
    ../lexlib/LexerNoExceptions.h
    ../lexlib/LexerSimple.h
    ../lexlib/OptionSet.h
    ../src/UnicodeFromUTF8.h
    ../lexlib/PropSetSimple.h
    ../lexlib/StyleContext.h
    ../lexlib/SubStyles.h
    ../lexlib/WordList.h
    ../src/AutoComplete.h
    ../src/CallTip.h
    ../src/CaseConvert.h
    ../src/CaseFolder.h
    ../src/Catalogue.h
    ../src/CellBuffer.h
    ../src/CharClassify.h
    ../src/ContractionState.h
    ../src/Decoration.h
    ../src/Document.h
    ../src/Editor.h
    ../src/EditView.h
    ../src/EditModel.h
    ../src/MarginView.h
    ../src/ExternalLexer.h
    ../src/FontQuality.h
    ../src/Indicator.h
    ../src/KeyMap.h
    ../src/Style.h
    ../src/LineMarker.h
    ../src/Partitioning.h
    ../src/PerLine.h
    ../src/PositionCache.h
    ../src/RESearch.h
    ../src/RunStyles.h
    ../src/ScintillaBase.h
    ../src/Selection.h
    ../src/SplitVector.h
)
SET(SOURCES
    qsciscintilla.cpp
    qsciscintillabase.cpp
    qsciabstractapis.cpp
    qsciapis.cpp
    qscicommand.cpp
    qscicommandset.cpp
    qscidocument.cpp
    qscilexer.cpp
    #qscilexerbash.cpp
    #qscilexerbatch.cpp
    #qscilexercmake.cpp
    qscilexercpp.cpp
    #qscilexercsharp.cpp
    #qscilexercss.cpp
    qscilexerjson.cpp
    qscilexerxml.cpp
    qscilexercustom.cpp
    #qscilexerd.cpp
    #qscilexerdiff.cpp
    #qscilexerfortran.cpp
    #qscilexerfortran77.cpp
    qscilexerhtml.cpp
    #qscilexeridl.cpp
    #qscilexerjava.cpp
    qscilexerjavascript.cpp
    #qscilexerlua.cpp
    #qscilexermakefile.cpp
    #qscilexermatlab.cpp
    #qscilexeroctave.cpp
    #qscilexerpascal.cpp
    #qscilexerperl.cpp
    #qscilexerpostscript.cpp
    #qscilexerpov.cpp
    #qscilexerproperties.cpp
    qscilexerpython.cpp
    #qscilexerruby.cpp
    #qscilexerspice.cpp
    #qscilexersql.cpp
    #qscilexertcl.cpp
    #qscilexertex.cpp
    #qscilexerverilog.cpp
    #qscilexervhdl.cpp
    #qscilexerxml.cpp
    #qscilexeryaml.cpp
    #qscimacro.cpp
    #qsciprinter.cpp
    qscistyle.cpp
    qscistyledtext.cpp
    MacPasteboardMime.cpp
    InputMethod.cpp
    SciClasses.cpp
    SciAccessibility.cpp
    ListBoxQt.cpp
    PlatQt.cpp
    ScintillaQt.cpp
    ../lexers/LexA68k.cpp
    ../lexers/LexAbaqus.cpp
    ../lexers/LexAda.cpp
    ../lexers/LexAPDL.cpp
    ../lexers/LexAsm.cpp
    ../lexers/LexAsn1.cpp
    ../lexers/LexASY.cpp
    ../lexers/LexAU3.cpp
    ../lexers/LexAVE.cpp
    ../lexers/LexAVS.cpp
    ../lexers/LexBaan.cpp
    ../lexers/LexBash.cpp
    ../lexers/LexBasic.cpp
    ../lexers/LexBatch.cpp
    ../lexers/LexBullant.cpp
    ../lexers/LexCaml.cpp
    ../lexers/LexCLW.cpp
    ../lexers/LexCmake.cpp
    ../lexers/LexCOBOL.cpp
    ../lexers/LexCoffeeScript.cpp
    ../lexers/LexConf.cpp
    ../lexers/LexCPP.cpp
    ../lexers/LexCrontab.cpp
    ../lexers/LexCsound.cpp
    ../lexers/LexCSS.cpp
    ../lexers/LexD.cpp
    ../lexers/LexDiff.cpp
    ../lexers/LexECL.cpp
    ../lexers/LexEiffel.cpp
    ../lexers/LexErlang.cpp
    ../lexers/LexErrorList.cpp
    ../lexers/LexEScript.cpp
    ../lexers/LexFlagship.cpp
    ../lexers/LexForth.cpp
    ../lexers/LexFortran.cpp
    ../lexers/LexGAP.cpp
    ../lexers/LexGui4Cli.cpp
    ../lexers/LexHaskell.cpp
    ../lexers/LexHTML.cpp
    ../lexers/LexInno.cpp
    ../lexers/LexKix.cpp
    ../lexers/LexKVIrc.cpp
    ../lexers/LexLaTeX.cpp
    ../lexers/LexLisp.cpp
    ../lexers/LexLout.cpp
    ../lexers/LexLua.cpp
    ../lexers/LexMagik.cpp
    ../lexers/LexMake.cpp
    ../lexers/LexMarkdown.cpp
    ../lexers/LexMatlab.cpp
    ../lexers/LexMetapost.cpp
    ../lexers/LexMMIXAL.cpp
    ../lexers/LexModula.cpp
    ../lexers/LexMPT.cpp
    ../lexers/LexMSSQL.cpp
    ../lexers/LexMySQL.cpp
    ../lexers/LexNimrod.cpp
    ../lexers/LexNsis.cpp
    ../lexers/LexNull.cpp
    ../lexers/LexOpal.cpp
    ../lexers/LexOScript.cpp
    #../lexers/LexOthers.cpp
    ../lexers/LexPascal.cpp
    ../lexers/LexPB.cpp
    ../lexers/LexPerl.cpp
    ../lexers/LexPLM.cpp
    ../lexers/LexPO.cpp
    ../lexers/LexPOV.cpp
    ../lexers/LexPowerPro.cpp
    ../lexers/LexPowerShell.cpp
    ../lexers/LexProgress.cpp
    ../lexers/LexProps.cpp
    ../lexers/LexPS.cpp
    ../lexers/LexPython.cpp
    ../lexers/LexR.cpp
    ../lexers/LexRebol.cpp
    ../lexers/LexRuby.cpp
    ../lexers/LexRust.cpp
    ../lexers/LexScriptol.cpp
    ../lexers/LexSmalltalk.cpp
    ../lexers/LexSML.cpp
    ../lexers/LexSorcus.cpp
    ../lexers/LexSpecman.cpp
    ../lexers/LexSpice.cpp
    ../lexers/LexSQL.cpp
    ../lexers/LexSTTXT.cpp
    ../lexers/LexTACL.cpp
    ../lexers/LexTADS3.cpp
    ../lexers/LexTAL.cpp
    ../lexers/LexTCL.cpp
    ../lexers/LexTCMD.cpp
    ../lexers/LexTeX.cpp
    ../lexers/LexTxt2tags.cpp
    ../lexers/LexVB.cpp
    ../lexers/LexVerilog.cpp
    ../lexers/LexVHDL.cpp
    ../lexers/LexVisualProlog.cpp
    ../lexers/LexYAML.cpp
    ../lexers/LexDMIS.cpp
    ../lexers/LexHex.cpp
    ../lexers/LexRegistry.cpp
    ../lexers/LexDMAP.cpp
    ../lexers/LexJSON.cpp
    ../lexers/LexEDIFACT.cpp
    ../lexlib/Accessor.cpp
    ../lexlib/CharacterCategory.cpp
    ../lexlib/CharacterSet.cpp
    ../lexlib/LexerBase.cpp
    ../lexlib/LexerModule.cpp
    ../lexlib/LexerNoExceptions.cpp
    ../lexlib/LexerSimple.cpp
    ../lexlib/PropSetSimple.cpp
    ../lexlib/StyleContext.cpp
    ../lexlib/WordList.cpp
    ../lexers/LexBibTeX.cpp
    ../src/AutoComplete.cpp
    ../src/CallTip.cpp
    ../src/CaseConvert.cpp
    ../src/CaseFolder.cpp
    ../src/Catalogue.cpp
    ../src/CellBuffer.cpp
    ../src/CharClassify.cpp
    ../src/ContractionState.cpp
    ../src/Decoration.cpp
    ../src/Document.cpp
    ../src/Editor.cpp
    ../src/EditView.cpp
    ../src/EditModel.cpp
    ../src/MarginView.cpp
    ../src/ExternalLexer.cpp
    ../src/Indicator.cpp
    ../src/KeyMap.cpp
    ../src/LineMarker.cpp
    ../src/PerLine.cpp
    ../src/PositionCache.cpp
    ../src/RESearch.cpp
    ../src/RunStyles.cpp
    ../src/ScintillaBase.cpp
    ../src/Selection.cpp
    ../src/Style.cpp
    ../src/UniConversion.cpp
    ../src/ViewStyle.cpp
    ../src/XPM.cpp
)
SOURCE_GROUP(sources FILES ${HEADERS} ${HEADER_INCLUDE} ${SOURCES})
SET(TS_FILES qscintilla_cs.ts qscintilla_de.ts qscintilla_es.ts qscintilla_fr.ts qscintilla_pt_br.ts)
QT5_ADD_TRANSLATION(QM_FILES ${TS_FILES})
SOURCE_GROUP("translations" FILES ${TS_FILES})
SOURCE_GROUP("qm-files" FILES ${QM_FILES})

ADD_LIBRARY(${PROJECT_NAME} STATIC ${HEADERS} ${HEADER_INCLUDE} ${SOURCES} ${QM_FILES})
TARGET_LINK_LIBRARIES(${PROJECT_NAME} ${Qt5Core_LIBRARIES} ${Qt5Gui_LIBRARIES} ${Qt5Widgets_LIBRARIES} ${Qt5MacExtras_LIBRARIES})

SET(TARGET_INSTALL_DESTINATION lib)
SET(HEADERS_INSTALL_DESTINATION include)

INSTALL(TARGETS ${PROJECT_NAME} DESTINATION ${TARGET_INSTALL_DESTINATION} COMPONENT APPLICATIONS)
INSTALL_FILES_HIERARCHY(FILES ${HEADER_INCLUDE} DESTINATION ${HEADERS_INSTALL_DESTINATION})
