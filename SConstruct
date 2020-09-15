#!/usr/bin/env python

import os

vars = Variables('custom.py')
vars.Add(BoolVariable('coverage', 'Set to build for coverage analysis', 0))
vars.Add('append_buildpath', 'manual append to buildpath', '')

## Define project paths --------------------------------------------------------
root_path = os.path.abspath('.')
outpost_path = [os.path.join(root_path, 'contrib/outpost-core')]
print(outpost_path)
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
    PLATFORM='outpost',
    GTEST_SUPPORT_NEEDED='no',
    ENV=os.environ)
print(envGlobal['OS'])
print(envGlobal['toolpath'])

Help(vars.GenerateHelpText(envGlobal))

buildfolder = os.path.join(root_path, 'build')

if envGlobal['coverage']:
    envGlobal.Tool('compiler_hosted_gcc_coverage')
    envGlobal.Tool('settings_buildpath')
    envGlobal['BUILDPATH'] = os.path.abspath(os.path.join(buildfolder, module, 'test/coverage'))
else:
    envGlobal.Tool('compiler_hosted_gcc')
    envGlobal.Tool('settings_buildpath')
    envGlobal['BUILDPATH'] = os.path.abspath(os.path.join(buildfolder, 'test/unittest'))

if envGlobal['append_buildpath']:
    envGlobal['BUILDPATH'] = os.path.abspath(os.path.join(buildfolder, envGlobal['append_buildpath'] + '/' ))

envGlobal['BASEPATH'] = root_path
envGlobal['ROOTPATH'] = root_path
envGlobal['IPCPATH'] = root_path
#envGlobal['BUILDPATH'] = os.path.join(build_path, variant_dir)
envGlobal['BUILDPATH'] = build_path
envGlobal['BINPATH'] = os.path.join(envGlobal['BUILDPATH'], 'bin')
envGlobal['LIBINSTALLPATH'] = os.path.join(envGlobal['BUILDPATH'], 'lib')
envGlobal['LIBPATH'] = envGlobal['LIBINSTALLPATH']

subSConscripts = [
                  'contrib/outpost-core/modules/SConscript.library',
                  'SConscript',
                 ]
for subSConscript in subSConscripts:
    SConscript(subSConscript, exports='envGlobal', duplicate = 0)

env = envGlobal.Clone()
