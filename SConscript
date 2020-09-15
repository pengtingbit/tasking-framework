#!/usr/bin/env python

import os

Import('envGlobal')

envGlobal.Append(CPPPATH=[os.path.abspath('.') ])

# Build GoogleTest
googletest = os.path.join(envGlobal['BASEPATH'], 'contrib/googletest-fused')
envGlobal.Append(CPPPATH=[
    #os.path.abspath('%s' % googletest),
    googletest,
])

env = envGlobal.Clone()
env['CXXFLAGS_language'] = ['-std=c++98']

env.RemoveFromList('CCFLAGS_warning', [
    '-Wconversion',
    '-Wundef',
    '-Wmissing-declarations'])
env.RemoveFromList('CXXFLAGS_warning', '-Wold-style-cast')

files = env.Glob('%s/*.cc' % googletest)
objects = []
for file in files:
    objects.append(env.Object(file))
envGlobal.Append(objects={'googletest': objects})

libraryGmock = env.StaticLibrary('gtest', objects)
envGlobal.Install('$BUILDPATH/lib', libraryGmock)
envGlobal.Append(LIBS=['gtest'])

#SConscript(
#    os.path.join(envGlobal['BASEPATH'], 'contrib/outpost-core/modules/SConscript.library'),
#    exports='envGlobal')

SConscript(
    os.path.join(envGlobal['BASEPATH'], 'src/SConscript'),
    exports='envGlobal')

SConscript(
    os.path.join(envGlobal['BASEPATH'], 'test/SConscript'),
    exports='envGlobal')

env = envGlobal.Clone()

