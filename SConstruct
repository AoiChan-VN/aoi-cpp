#!/usr/bin/env python

import os
import sys

libname = "aoi_native"
projectdir = "project"

localEnv = Environment(tools=["default"], PLATFORM="")

# Xử lý custom.py một cách an toàn (không bắt buộc phải tồn tại)
customs = []
if os.path.exists("custom.py"):
    customs = [os.path.abspath("custom.py")]

opts = Variables(customs, ARGUMENTS)
opts.Update(localEnv)
Help(opts.GenerateHelpText(localEnv))

env = localEnv.Clone()

# Kiểm tra godot-cpp submodule
if not (os.path.isdir("godot-cpp") and os.listdir("godot-cpp")):
    print("ERROR: godot-cpp is not available within this folder, as Git submodules haven't been initialized.")
    print("Run the following command to download godot-cpp:")
    print("git submodule update --init --recursive")
    sys.exit(1)

env = SConscript("godot-cpp/SConstruct", {"env": env, "customs": customs})
env.Append(CPPPATH=["src/"])

sources = Glob("src/*.cpp")

if env["target"] in ["editor", "template_debug"]:
    try:
        doc_data = env.GodotCPPDocData("src/gen/doc_data.gen.cpp", source=Glob("doc_classes/*.xml"))
        sources.append(doc_data)
    except AttributeError:
        print("Not including class reference as we're targeting a pre-4.3 baseline.")

suffix = env['suffix'].replace(".dev", "").replace(".universal", "")
lib_filename = "{}{}{}{}".format(env.subst('$SHLIBPREFIX'), libname, suffix, env.subst('$SHLIBSUFFIX'))

library = env.SharedLibrary(
    "bin/{}/{}".format(env['platform'], lib_filename),
    source=sources,
)

copy = env.Install("{}/bin/{}/".format(projectdir, env["platform"]), library)
default_args = [library, copy]
Default(*default_args)
