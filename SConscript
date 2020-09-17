#!/usr/bin/env python

import os

Import('envGlobal')

SConscript(
    os.path.join(envGlobal['BASEPATH'], 'src/SConscript'),
    exports='envGlobal')

SConscript(
    os.path.join(envGlobal['BASEPATH'], 'test/SConscript'),
    exports='envGlobal')

env = envGlobal.Clone()

