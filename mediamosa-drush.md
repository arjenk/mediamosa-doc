### Drush

Drush is a shell command line interface to a Drupal application. Since
MediaMosa is based on Drupal, you can use any drush command on
MediaMosa. Examples of such generic commands are;

* ```drush cache-clear all```
  Cleares all caching tables;
* ```drush wd-show --tail```
  Shows the message log on the commandline

MediaMosa also has some specific drush commands supported for basic
operations. For example;

* ```drush mm-asset-list```
  Gives a list of assets
* ```drush mm-transcode <mediafile_id> <profile_id>```
  Starts a transcode job with profile id for a mediafile.

A full list of MediaMosa commands can be found when running drush without parameters.

#### How to install

MediaMosa drush does not have specific requirements for the drush
version. A normal install will work. For example the debian drush
package will work just fine. More installation instructions are found
on the drush site: https://drupal.org/node/1791676

See also the drush faq: [https://drupal.org/drush-faq](https://drupal.org/drush-faq)

