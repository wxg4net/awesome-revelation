# revelation.lua

Provides Mac OSX like 'Expose' view of all clients. 
It is modified from the original revelation.lua. 

##Changes from the original revelation
* Support awesome 3.5 or later 

* Add support of multiple screens. Now the revelation will be trigged on
  the on the multiple screens at the same time.

* The way of selecting and activing  the client was changed. Navigating
  clients by the keys "j,h,k,l"  and then selecting the client by key "Enter" was
  deprecated. Now the ways of selecting and activing is the same to the way in
  the module hint.

* Add zoom mode. Add the function of zooming the client by pressing the right
  button of the mouse.

* The unwanted clients can be excluded by rules. 

## Use

### Installation
 (From user's awesome configuration directory, usually ~/.config/awesome)

 1. Clone repository:

        git clone https://github.com/guotsuan/awesome-revelation.git

 2. put near the top of your rc.lua `local revelation=require("revelation")`

 3. put the revelation.init() after the beautiful.init()

 3. Make a global keybinding (ModKey + e) for revelation in your rc.lua:

        globalkeys = awful.util.table.join(
        awful.key({ modkey,           }, "Left",   awful.tag.viewprev       ), 
        awful.key({ modkey,           }, "Right",  awful.tag.viewnext       ),
        awful.key({ modkey,           }, "Escape", awful.tag.history.restore),
        awful.key({ modkey}, "e", revelation),  -- Insert this line

        awful.key({ modkey,           }, "j",
        function ()
            awful.client.focus.byidx( 1)
            if client.focus then client.focus:raise() end
        end),

    **NOTE:** Always double check this key binding syntax against the version of
    Awesome that you are using.

 4. Reload rc.lua and try the keybinding __Modkey + e__

 It should bring all clients to the current tags on all screens and set the layout to fair.
 You  can focus clients with __cursor__ then press the left button to select, or select by 
pressing the keys shown in the hint boxs. Press the mouse right button to zoom the client 
or __Escape__ to abort.

### Configuration
 Revelation's configuration is done through direct access to the module's
 `config` table.

 There are two basic settings, shown with default values:

    -- The name of the tag created for the 'exposed' view
    revelation_config.tag_name = 'Revelation'

    -- A table of matcher functions (used in client filtering)
    revelation_match.exact = awful.rules.match
    revelation_match.any   = awful.rules.match_any

 The rule matching functions must conform to `awful.rules.match` prototypes.

 For client matching rules, we follow the same syntax as awful.rules with one
 perk; if `rule.any == true`, then we call the `config.match.any` function.


### Examples
 All clients:

     awful.key({modkey}, "e", revelation)

 To match all urxvt terminals:

     awful.key({modkey}, "e", function()
                revelation({class="URxvt"})
             end)
 To match clients with class 'foo' or 'bar':

     awful.key({modkey}, "e", function()
                revelation({
                            class={"foo", "bar"},
                            any=true
                            })
            end)

 To exclude the clients,  we set:

     awful.key({modkey}, "e", function()
             revelation({class="conky"}, is_excluded=true)
             end)

## Credits

### Maintenance
    * Quan Guo <guotsuan@gmail.com>
    * Perry Hargrave <resixian@gmail.com>

### Contributions, many thanks!
    * Nikola Petrov <nikolavp@gmail.com>

### Original authors
    * Espen Wiborg <espenhw@grumblesmurf.org>
    * Julien Danjou <julien@danjou.info>

## License
    Revelation is released under the GNU General Public License, version 3.
    (c) 2009-12 Perry Hargrave
    (c) 2008 Espen Wiborg, Julien Danjou
