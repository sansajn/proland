import os

AddOption('--debug-build', action='store_true', dest='debug_build', 
	default=False)

env = Environment()
#env['CXX'] = 'clang++'
#env['ENV']['TERM'] = os.environ['TERM']

# core
if GetOption('debug_build'):
	env.Append(CPPFLAGS = ['-g', '-O0', '-DDEBUG', '-std=c++98'])
else:
	env.Append(CCFLAGS=['-Os', '-std=c++98'])

env.Append(
	CCFLAGS = ['-DORK_API=', '-DTIXML_USE_STL', '-DPROLAND_API='],
	CPPPATH = [
		'atmo/sources',
		'core/sources',
		'edit/sources',
		'forest/sources',
		'graph/sources', 
		'ocean/sources',
		'river/sources',
		'terrain/sources',
		'../anttweakbar/include', 
		'../ork',
		'../ork/libraries'],
)

core_path = 'core/sources/proland/'

core_math_objs = env.Object(Glob(core_path+'math/*.cpp'))
core_producer_objs = env.Object(Glob(core_path+'producer/*.cpp'))
core_terrain_objs = env.Object(Glob(core_path+'terrain/*.cpp'))
core_util_objs = env.Object(Glob(core_path+'util/*.cpp'))

particles_path = core_path+'particles/'
core_particles_objs = env.Object([
	Glob(particles_path+'/*.cpp'),
	Glob(particles_path+'screen/*.cpp'),
	Glob(particles_path+'terrain/*.cpp')]
)

ui_path = core_path+'ui/'
core_ui_objs = env.Object([
	Glob(ui_path+'*.cpp'), Glob(ui_path+'twbar/*.cpp')])

core_objs = [
	core_math_objs,
	core_producer_objs,
	core_terrain_objs,
	core_util_objs,
	core_particles_objs,
	core_ui_objs]	


# terrain
terrain_path = 'terrain/sources/proland/'

terrain_objs = env.Object([
	Glob(terrain_path+'*.cpp'),
	Glob(terrain_path+'dem/*.cpp'),
	Glob(terrain_path+'ortho/*.cpp'),
	Glob(terrain_path+'preprocess/terrain/*.cpp')]
)

# graph
graph_path = 'graph/sources/proland/'
graph_objs = env.Object([
	Glob(graph_path+'dem/*.cpp'),
	Glob(graph_path+'graph/*.cpp'),
	Glob(graph_path+'graph/producer/*.cpp'),
	Glob(graph_path+'ortho/*.cpp'),
	Glob(graph_path+'*.cpp')])

# atmo
atmo_objs =	env.Object(
	Glob('atmo/sources/proland/preprocess/atmo/*.cpp'))

# ocean
ocean_path = 'ocean/sources/proland/'
ocean_objs = env.Object([
	ocean_path + 'OceanPlugin.cpp',
	Glob(ocean_path + 'ocean/*.cpp')])

# edit
edit_path = 'edit/sources/proland/'

edit_objs = env.Object([
	Glob(edit_path+'*.cpp'),
	Glob(edit_path+'edit/*.cpp')])

edit_twbar_objs = env.Object([
	Glob(edit_path+'ui/twbar/*.cpp')])

#river
river_path = 'river/sources/proland/'

river_objs = env.Object([
	Glob(river_path+'*.cpp'),
	Glob(river_path+'rivers/*.cpp'),
	Glob(river_path+'rivers/graph/*.cpp')])

river_twbar_objs = env.Object([
	Glob(river_path+'ui/twbar/*.cpp')])

#forest
forest_path = 'forest/sources/proland/'

forest_objs = env.Object([
	Glob(forest_path + '*.cpp'),
	Glob(forest_path + 'plants/*.cpp'),
	Glob(forest_path + 'preprocess/trees/*.cpp')])


# examples

# core:examples
common_libs = ['GL', 'GLU', 'glut', 'GLEW', 'X11', 'tiff', 'pthread']

env.Program([
	'core/examples/helloworld/HelloWorld.cpp', 
	core_objs],
	LIBS = ['ork', 'anttweakbar', common_libs],  # TODO: don't we have pkg-config for ork and anttweakbar?
)

# terrain:examples
terrain_examples_common = [
	core_objs, 
	graph_objs,
	terrain_objs,
	ocean_objs,
	atmo_objs,
	edit_objs,
	river_objs,
	forest_objs,
]

terrain_libs = ['ork', 'anttweakbar', common_libs]

for n in range(1,6):
	env.Program([
		'terrain/examples/exercise%d/HelloWorld.cpp' % (n, ),
		terrain_examples_common],
		LIBS = terrain_libs
	)


for n in range(1,6):
	env.Program([
		'terrain/examples/terrain%d/HelloWorld.cpp' % (n, ),
		terrain_examples_common],
		LIBS = terrain_libs
	)


env.Program([
	'terrain/examples/preprocess/HelloWorld.cpp',
	terrain_examples_common],
	LIBS = terrain_libs
)


# graph:examples
env.Program([
	'graph/examples/graph1/HelloWorld.cpp',
	core_objs, 
	terrain_objs,
	graph_objs],
	LIBS = ['ork', 'anttweakbar', common_libs],
	LIBPATH = ['../anttweakbar']
)


