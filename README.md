<center>
<h2>Mod App Creator</h2>
</center>
<p><strong>Require:</strong><br />- STALKER-Anomaly-modded-exes version at least 2025.08.23: <a href="https://github.com/themrdemonized/xray-monolith">Github.com</a><br />- <a href="https://www.moddb.com/mods/stalker-anomaly/addons/anomaly-mod-configuration-menu">MCM</a><br /><br /><strong>Useful addon-reletad links:</strong><br />- <a href="https://discord.com/channels/912320241713958912/1419250864807219280">G.A.M.M.A. Discord topic</a><br />- <a href="https://discord.com/channels/456765861953536020/1419250183019036732">Anomaly Discord topic</a><br />- <a href="https://github.com/Ncenka/Mod-App-Creator/">GitHub</a><br /><br /><strong>Integrations:</strong><br />- <a href="https://www.moddb.com/mods/stalker-anomaly/addons/3d-interactive-pda-18-release">PDA Interactive</a><br />- <a href="https://www.moddb.com/mods/stalker-anomaly/addons/itheons-pda-taskboard">Taskboard</a><br />- <a href="https://www.moddb.com/mods/stalker-anomaly/addons/fatal-error-by-ncenka">Fatal Error</a><br />- PANDA Private Messages (to be released)</p>
<p>Tired of dealing with conflicts and compatibility issues when creating new PDA tabs? Introducing the Mod App Creator (MAC) framework - a unified solution for extending PDA functionality without the headache of patching.</p>
<p>MAC provides a streamlined framework for seamlessly integrating new PDA tabs (apps) into a unified Launcher interface. No more incompatibilities and endless patches - framework offers a clean, standardized approach to PDA tabs (apps).<br /><br /><img src="https://media.moddb.com/images/members/5/4252/4251450/profile/2025-09-2.png" alt="" /></p>
<p>Key Features:<br />- Launcher: All new tabs (apps) can be organized in one UI tab.<br />- Zero Conflicts (at least i hope): No more incompatibilities or overlapping patches.<br />- Easy Integration: Add new tabs (apps) with minimal code.<br />- Auto Monkey Patching: MAC will automatically create a patch for your tab in <strong>pda.script</strong>.</p>
<p>Example:</p>
<pre><code>mac_mcm.add_app("your_app_id", {
     name = "st_app_name", -- Unlocalized string.
     texture = "app_texture", -- Texture
     tab = "eptApp" -- Your PDA tab section
     func = ui_pda_taskboard_tab.get_ui -- Function to call
})</code></pre>
<p>To fix disappearing top bar use dxml to inject code like this into <strong>pda_16.xml</strong>:</p>
<pre><code>function on_xml_read()
    RegisterScriptCallback("on_xml_read", on_xml_read_callback)
end

function on_xml_read_callback(file_name, xml_obj)
    -- Check if its the file i want to change
    if file_name == [[ui\pda_16.xml]] then
        -- Here is my code to change XML
        local new_tab = [[
&lt;button x="1000" y="0" width="0" height="0" id="eptYourTab" frame_mode="0"&gt;
    &lt;text align="c" vert_align="c" x="0" y="0" font="letterica16"&gt;pda_btn_your_button&lt;/text&gt;
&lt;/button&gt;
]]
        local res = xml_obj:query("tab")
        if is_not_empty(res) then
            local el = res[1]
            xml_obj:insertFromXMLString(new_tab, el, #el.kids)
        end
    end

    
end</code></pre>
<p>Or just use Launcher key to get back to Main Launcher tab (Right Control by Default, MCM configurable). Also you can ask me and i will just include it, like i've done with Taskboard or Interactive.</p>
<p>Changelog:<br />08/03/2026 - 0.9.9.3<br />- Integration for PANDA Private Messages (to be released).<br /><br />23/09/2025 - 0.9.9.2<br />- Assert simplification.<br />- <strong>remove_app</strong> and <strong>remove_blocked_tabs</strong> added.<br />- <strong>reload_interface</strong> added for reloading interface when needed.<br />- Additional check for <strong>bind_launcher</strong>.<br /><br />21/09/2025 - 0.9.9.1<br />- Initial Release.</p>
