#!/usr/bin/env python

import os

vars = Variables('custom.py')
vars.Add(BoolVariable('coverage', 'Set to build for coverage analysis', 0))
vars.Add('append_buildpath', 'manual append to buildpath', '')

## Define project paths --------------------------------------------------------
root_path = os.path.abspath('.')
build_path = os.path.join(root_path, 'build')

envGlobal = Environment(
    CXXFLAGS=["-std=c++11", "--debug"],
    toolpath=[os.path.join(root_path, 'contrib/scons-build-tools/site_tools')],
    tools=['compiler_hosted_gcc',
           'settings_buildpath',
           'utils_buildformat',
           'utils_buildsize'],
    variables=vars,
    BASEPATH=os.path.abspath('.'),
    OS='posix',
    PLATFORM='linux',
    GTEST_SUPPORT_NEEDED='yes',
    ENV=os.environ)

Help(vars.GenerateHelpText(envGlobal))

buildfolder = os.path.join(root_path, 'build')

envGlobal['BASEPATH'] = root_path
envGlobal['ROOTPATH'] = root_path
envGlobal['IPCPATH'] = root_path
envGlobal['BUILDPATH'] = build_path
envGlobal['BINPATH'] = os.path.join(envGlobal['BUILDPATH'], 'bin')
envGlobal['LIBINSTALLPATH'] = os.path.join(envGlobal['BUILDPATH'], 'lib')
envGlobal['LIBPATH'] = envGlobal['LIBINSTALLPATH']

if envGlobal['PLATFORM'] == 'outpost':
    subSConscripts = [
                         'contrib/outpost-core/modules/SConscript.library',
                         'SConscript',
                     ]
else:
    subSConscripts = [
                         'SConscript',
                     ]
for subSConscript in subSConscripts:
    SConscript(subSConscript, exports='envGlobal', duplicate = 0)

env = envGlobal.Clone()
