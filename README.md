# Manage-User-Roles-on-WP
This code snippet was developed to create an additional role for wp user who want to have more user roles than an editor but not a complete administrator role.
Copy below code and paste on your function file.It will create new site owner capabilities.


<?php
add_action('after_setup_theme',function(){
    if(! get_option('wpc_role_created')){
$site_owner_caps = get_role('administrator')->capabilities;
$unwanted_caps = [
    'switch_themes' => 1,
    'delete_pages' => 1,
    'edit_plugins' => 1,
    'update_core' => 1,
     'update_themes' => 1,
     'delete_themes' => 1,
    'install_themes' => 1,
    'update_plugins' => 1,
    'delete_plugins' => 1,
        ];

$site_owner_caps = array_diff_key($site_owner_caps,$unwanted_caps);

   add_role('site_owner','site owner',$site_owner_caps);
   update_option('wpc_role_created',true);
   
    }
});



