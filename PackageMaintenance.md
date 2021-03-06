## Updating and Upgrading Raspbian 

### Routine "in-version" updates and upgrades

<html>
<head>

</head>

<body>
<table class="minimalistBlack">
<thead>
<tr>
<th>Command</th>
<th>Explanation</th>
</tr>
</thead>
<tbody>

<tr>
<td width="30%"> <b><code>df -h</code></b></td>
<td width="70%">check available space; <code>apt</code> doesn't do this automatically, so it's up to you</td>
</tr>   
<tr>
<td><b><code>sudo apt-get update</code></b></td>
<td>updates the system's "Package List"</td>
</tr>

<tr>
<td><b><code>sudo apt-get upgrade</code></b></td>
<td>upgrade all installed packages to the latest version from the sources enumerated in  <code>/etc/apt/sources.list</code>, but under no circumstances are currently installed packages removed, or packages not already installed retrieved and installed. <em>This is the "foolproof" version of an upgrade.</em></td>
</tr>
<tr>
<td><b><code>sudo apt-get dist-upgrade</code></b></td>
<td>upgrade all installed packages to the latest version from the sources enumerated in  <code>/etc/apt/sources.list</code>. It will add & remove packages if necessary, and attempts to deal "intelligently" with changed dependencies. Exceptions may be declared in <code>apt_preferences(5)</code>.</td>
</tr>
<tr>
   <td><b><code>sudo apt-get clean</code></b></td>
<td>removes the cruft from <code>/var/cache/apt/archives</code> left by previous upgrades</td>
</tr>
<tr>
   <td><b><code>sudo reboot</code></b></td>
<td>when in doubt, or if "weird" things happen! [REFERENCE](https://www.raspberrypi.org/forums/viewtopic.php?t=184850)</td>
</tr> 
<tr>
<td> </td>
<td> </td>
</tr>
<tr>
<td> </td>
<td> </td>
</tr>   
</tbody>
</table>




### Version Upgrade

To do an in-place upgrade of the OS; e.g. from jessie to stretch:

Opinions vary on the details, but in general: (note: `sudo` needed for all commands, but omitted for brevity): 

1. `sudo apt-get update`,	`... upgrade`,		 `... dist-upgrade`

2. Verify no issues exist in previous updates or upgrades:
   `dpkg --audit`
   `dpkg --get-selections | grep hold`
   
3. BACKUP!!!

4. change `jessie` to `stretch in `/etc/apt/sources.list` 

5. `... update`, `... upgrade`, `... dist-upgrade` again (which may take a while!)

6. `reboot`

7. `cat /etc/os-release` to verify the upgrade was successful 


NOTE: This recipe augments [one at the raspberrypi.org website on the same subject](https://www.raspberrypi.org/documentation/raspbian/updating.md), and from [this source for linux tutorials](https://www.howtoforge.com/tutorial/how-to-upgrade-debian-8-jessie-to-9-stretch/)

## Installing and Removing Packages using `apt` 

Some advocate using `apt`, others advocate using `apt-get`. At present, I favor `apt-get` if only because I'm used to it. The diffs aren't worth much discussion, but you will need to decide. [Here's one explanation that might help](https://itsfoss.com/apt-vs-apt-get-difference/), and there are many others available for the [cost of a search.](https://duckduckgo.com/?q=apt+vs+apt-get&t=ffnt&ia=web) 

<table class="minimalistBlack">
<thead>
<tr>
<th>Command</th>
<th>Explanation</th>
</tr>
</thead>
<tbody>

<tr>
<td width="30%"> <b><code>sudo apt-get install XXXX</code></b></td>
<td width="70%">Install a package "XXXX"</td>
</tr>   

<tr>
<td width="30%"> <b><code>sudo apt-get remove XXXX</code></b></td>
<td width="70%">Remove a package "XXXX", leaving its configuration files on the system</td>
</tr>

<tr>
<td width="30%"> <b><code>sudo apt-get purge XXXX</code></b></td>
<td width="70%">Remove a package "XXXX", deleting its configuration files from the system</td>
</tr>

</tbody>
</table>
</body>
</html>

## Frequently Useful Commands in Aptitude

`apt-cache search XXXX`  

> list available packages whose names contain the word or characters `XXXX`. For example if you're looking for a package, and you recall that its name contains the characters `priv`, then `apt-cache search priv` should list all matching packages in the repository for RPi.

Listing installed packages: 

    sudo apt list --installed   
    dpkg --get-selections 
    dpkg -l  



## REFERENCES: 

1. [Debian CLI for APT package management tools](https://wiki.debian.org/AptCLI) 

<!--- 


| &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Command &nbsp; &nbsp;  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; | Explanation |
| :---     | :---       |
| `sudo apt-get update`| updates the system's "Package List" |
| `df -h`      | check available space; `apt` doesn't! |
| `sudo apt-get upgrade` | upgrade all installed packages to the latest version from the sources enumerated in  `/etc/apt/sources.list`, but under no circumstances are currently installed packages removed, or packages not already installed retrieved and installed. This is the "foolproof" version of an upgrade. |
| `sudo apt-get dist-upgrade` | upgrade all installed packages to the latest version from the sources enumerated in  `/etc/apt/sources.list`. It will add & remove packages if necessary, and attempts to deal "intelligently" with changed dependencies. Exceptions may be declared in `apt_preferences(5)`. |
| `sudo apt-get clean` | removes the cruft from `/var/cache/apt/archives` left by previous upgrades |
| `sudo reboot` | when in doubt, or if "weird" things happen! [REFERENCE](https://www.raspberrypi.org/forums/viewtopic.php?t=184850) |


__-------------  WORK IN PROCESS; PLEASE IGNORE (or not - up to you!) -----------------__

<!DOCTYPE html>
<html>
<head>

<style>
table.minimalistBlack {
  width: 100%;
  text-align: left;
  border-collapse: collapse;
}
table.minimalistBlack td, table.minimalistBlack th {
  border: 1px solid #000000;
  padding: 5px 4px;
}
table.minimalistBlack tbody td {
  font-size: 13px;
}
table.minimalistBlack tr:nth-child(even) {
  background: #CFD1D1;
}
table.minimalistBlack thead {
  background: #CFCFCF;
  background: -moz-linear-gradient(top, #dbdbdb 0%, #d3d3d3 66%, #CFCFCF 100%);
  background: -webkit-linear-gradient(top, #dbdbdb 0%, #d3d3d3 66%, #CFCFCF 100%);
  background: linear-gradient(to bottom, #dbdbdb 0%, #d3d3d3 66%, #CFCFCF 100%);
  border-bottom: 2px solid #000000;
}
table.minimalistBlack thead th {
  font-size: 15px;
  font-weight: bold;
  color: #000000;
  text-align: center;
}
table.minimalistBlack tfoot td {
  font-size: 14px;
}
</style>
</head>

<body>
<table class="minimalistBlack">
<thead>
<tr>
<th>head1</th>
<th>head2</th>
</tr>
</thead>
<tbody>
<tr>
<td>cell1_1</td>
<td>cell2_1</td>
</tr>
<tr>
<td>cell1_2</td>
<td>cell2_2</td>
</tr>
<tr>
<td>cell1_3</td>
<td>cell2_3</td>
</tr>
<tr>
<td>cell1_4</td>
<td>cell2_4</td>
</tr>
<tr>
<td>cell1_5</td>
<td>cell2_5</td>
</tr>
</tbody>
</table>
</body>
</html>

-->
