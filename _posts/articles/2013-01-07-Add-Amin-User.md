---
published: true
layout: article
title: Add Amin User
abstract: Magento Cheat Sheet, how to add a magento admin user, directly thorugh SQL
author_twitter: Fabian_ikono
author: Fabian Blechschmidt
categories:
- articles
---

Thanks to [Atwix](http://www.atwix.com), i found the [SQL which is needed to create a magento admin user](http://www.atwix.com/magento/reset-admin-password-mysql/).

Cheat sheet for me:

	SET @fistname = 'Fabian';
    SET @lastname = 'Blechschmidt';
    SET @email = 'mailaddress@example.com';
    SET @username = 'fabian';
    SET @password = 'password';
    SET @salt = 'Fl';
    
    INSERT INTO admin_user
    SELECT
    NULL user_id,
    @fistname firstname,
    @lastname lastname,
    @email email,
    @username username,
    CONCAT(MD5(CONCAT(@salt, @password)), ':', @salt) password,
    NOW( ) created,
    NULL modified,
    NULL logdate,
    0 lognum,
    0 reload_acl_flag,
    1 is_active,
    (SELECT MAX(extra) FROM admin_user WHERE extra IS NOT NULL) extra,
    NULL rp_token,
    NOW() rp_token_created_at;
    
    INSERT INTO admin_role
    SELECT
    NULL role_id,
    (SELECT role_id FROM admin_role WHERE role_name = 'Administrators') parent_id,
    2 tree_level,
    0 sort_order,
    'U' role_type,
    (SELECT user_id FROM admin_user WHERE username = @username) user_id,
    @username role_name