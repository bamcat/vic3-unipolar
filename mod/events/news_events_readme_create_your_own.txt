namespace = news

# ══════════════════════════════════════════════════════════════════════
# test events, ignore. For those who want to make their own news events, just use gui_window = news_event_window. It's that simple.  But there's more, obviously:
#
# news_set_masthead_id = yes -> enables country-specific mastheads
# news_pick_title_variant = yes -> allows for titles to change for the same news story
# news_headline_quiet = yes -> mostly-lowercase headline instead of all uppercase
# news_headline_major = yes -> all-uppercase news title
# all of the above goes into the immediate box
# in order for the mod to work, the fonts folder is required.
# ══════════════════════════════════════════════════════════════════════

#  TEST CLIPPING 
news.1 = {
	type = country_event
	placement = ROOT

	title = news.1.t
	desc = news.1.d
	flavor = news.1.f

	duration = 3

	gui_window = news_event_window

	event_image = { video = "unspecific_signed_contract" }

	on_created_soundeffect = "event:/SFX/UI/Alerts/event_appear"
	icon = "gfx/interface/icons/event_icons/waving_flag.dds"

	trigger = { }

	immediate = {
		news_set_masthead_id = yes
	}

	option = {
		name = news.1.a
		default_option = yes
	}
}

#  WAR DECLARED 
# Fired manually for now; an on_action would capture the real belligerents
# and pass them in as scopes exactly the same way.
news.2 = {
	type = country_event
	placement = ROOT

	title = news.2.t
	desc = news.2.d
	flavor = news.2.f

	duration = 3

	gui_window = news_event_window

	event_image = { video = "europenorthamerica_before_the_battle" }

	on_created_soundeffect = "event:/SFX/UI/Alerts/event_appear"
	icon = "gfx/interface/icons/event_icons/event_war.dds"

	trigger = { }

	immediate = {
		news_set_masthead_id = yes
		# Fill the belligerents if they were not supplied, so the event is
		# testable straight from the console.
		if = {
			limit = { NOT = { exists = scope:news_attacker } }
			save_scope_as = news_attacker
			random_country = {
				limit = { NOT = { this = root } exists = capital }
				save_scope_as = news_defender
			}
		}
	

	    if = { limit = { exists = scope:news_attacker } set_variable = { name = news_test_2_news_attacker_ref value = scope:news_attacker months = 4 } }
	    var:news_test_2_news_attacker_ref ?= { save_scope_as = news_error_log_silencer } # Silence localization-only variable warning.

	    if = { limit = { exists = scope:news_defender } set_variable = { name = news_test_2_news_defender_ref value = scope:news_defender months = 4 } }
	    var:news_test_2_news_defender_ref ?= { save_scope_as = news_error_log_silencer } # Silence localization-only variable warning.

	}

	option = {
		name = news.2.a
		default_option = yes
	}
}
