AM_CPPFLAGS = \
	-I$(top_srcdir) \
	-DG_LOG_DOMAIN=\"multiload-ng-mate\" \
	-DPACKAGE_LOCALE_DIR=\"$(localedir)\" \
	-DMATELOCALEDIR=\"$(localedir)\" \
	$(PLATFORM_CPPFLAGS)


libexec_PROGRAMS = mate-multiload-ng-applet
mate_multiload_ng_applet_LOCATION = \
	$(libexecdir)/mate-multiload-ng-applet

mate_multiload_ng_applet_SOURCES = \
	plugin.c

mate_multiload_ng_applet_CFLAGS = \
	$(GTK_CFLAGS) \
	$(MATE_CFLAGS)

# TESTING CFLAGS: uncomment to enable debugging (gdb) and profiling (gprof)
#mate_multiload_ng_applet_CFLAGS += -pg -ggdb -O0

mate_multiload_ng_applet_LDADD = \
	$(GTK_LIBS) \
	$(MATE_LIBS) \
	-lm \
	../common/multiload-ng-core.la


plugindir = $(datadir)/mate-panel/applets
plugin_in_files = org.mate.multiload-ng.Applet.mate-panel-applet.in
plugin_DATA     = $(plugin_in_files:.mate-panel-applet.in=.mate-panel-applet)

$(plugin_in_files): $(plugin_in_files).in Makefile
	$(AM_V_GEN)sed -e "s|\@LOCATION\@|$(mate_multiload_ng_applet_LOCATION)|" $< > $@

org.mate.multiload-ng.Applet.mate-panel-applet: org.mate.multiload-ng.Applet.mate-panel-applet.in
	$(INTLTOOL_MERGE) $(top_srcdir)/po $< $@ -d -u -c $(top_builddir)/po/.intltool-merge-cache
#	$(INTLTOOL_MERGE) $(wildcard $(top_srcdir)/po/*po)

servicedir       = $(datadir)/dbus-1/services
service_in_files = org.mate.panel.applet.MultiloadNgFactory.service.in
service_DATA     = $(service_in_files:.service.in=.service)

org.mate.panel.applet.MultiloadNgFactory.service: $(service_in_files)
	$(AM_V_GEN)sed -e "s|\@LOCATION\@|$(mate_multiload_ng_applet_LOCATION)|" $< > $@


@INTLTOOL_XML_NOMERGE_RULE@
multiload_gschema_in_files = org.mate.panel.applet.multiload-ng.gschema.xml.in
gsettings_SCHEMAS = $(multiload_gschema_in_files:.xml.in=.xml)
@GSETTINGS_RULES@

EXTRA_DIST = \
	$(plugin_in_files) \
	$(service_in_files) \
	$(multiload_gschema_in_files)

CLEANFILES = \
	org.mate.multiload-ng.Applet.mate-panel-applet \
	org.mate.panel.applet.MultiloadNgFactory.service \
	org.mate.panel.applet.multiload-ng.gschema.xml \
	$(plugin_in_files)

# vi:set ts=8 sw=8 noet ai nocindent syntax=automake: