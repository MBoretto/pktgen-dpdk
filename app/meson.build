sources = files(
	'pktgen-cmds.c', 'pktgen.c', 'pktgen-cfg.c',
	'pktgen-main.c', 'pktgen-pcap.c', 'pktgen-range.c', 'pktgen-cpu.c',
	'pktgen-seq.c', 'pktgen-dump.c', 'pktgen-capture.c', 'pktgen-stats.c',
	'pktgen-port-cfg.c', 'pktgen-ipv4.c', 'pktgen-arp.c',
	'pktgen-ether.c', 'pktgen-udp.c', 
	'pktgen-random.c', 'pktgen-display.c', 'pktgen-log.c',
	'pktgen-latency.c', 'pktgen-rate.c'
)

if get_option('enable_gui')
    sources += files(
        'pktgen-gui.c',
        'pktgen-gui-misc.c',
        'pktgen-gui-streams.c',
    )
endif

cflags = ['-D__PROJECT_VERSION="' + meson.project_version() + '"']

deps = [dpdk, common, cli, utils]

if get_option('enable_gui')
    deps += dependency('glib-2.0', required: true)
    deps += dependency('gtk+-2.0', required: true)
    cflags += '-Wno-deprecated-declarations'
    cflags += '-DGUI'
endif

deps += [dependency('threads')]
deps += [cc.find_library('numa', required: true)]
deps += [cc.find_library('pcap', required: true)]
deps += [cc.find_library('dl', required: false)]
deps += [cc.find_library('m', required: false)]

pktgen = executable('pktgen',
		sources,
		c_args: cflags,
		install: true,
		dependencies: [deps, lua_dep])
