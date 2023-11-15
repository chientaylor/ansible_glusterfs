# ansible_glusterfs

A basic rough build for a small four-node Gluster Cluster with one disk each. This was used to build a cluster with a set of four ROCK64 SBCs each with an SSD connected to a USB-SATA adapter. The purpose of this was to test the basics of a clustered file system on a set of ARM devices.

## Definitions

`gluster_disk_device` - String - Required - The device to be used as the backing store. Needs to be in the `/dev/disk/by-id/` format.

`gluster_volume_names` - List - Required - The bricks to create. Can be just one or several. Will all use the single disk as a backing store.

`gluster_force_disk_partitioning_delete_everything` - Default: Empty String - Set this to "DELETE" to allow the deletion of the partitions of the target disk

`gluster_force_disk_partitioning_make_it_go_away` - Default: Empty String - Set this to "GOAWAY" to allow the deletion of the partition of the target disk

`gluster_pool_name` - Default: "storage" - Used as the name of the mount point (/storage by default)

`gluster_volume_name` - Default: "gluster" - Used as the name of the folder/dataset where the bricks are stored

`gluster_backing_zfs` - Default: False - If ZFS is used, a different task will be run to set that up. This only sets ZFS up on the single disk defined in the `gluster_disk_device` variable. Not used by default due to issues with the custom Armbian kernels.

`gluster_disk_fs` - Default: "xfs" - By default use XFS filesystem. This must be a valid filesystem type usable by the system, so refer to the fstype list.

`gluster_pool_replicas` - Default: 2 - The number of replicas to have in the Gluster volume.

`linux_headers_default` - Default: True - Used to mark when the default architecture kernel headers are acceptable. This will not work for some ARM builds.

`kernel_headers_package` - Optional - Overrides the package used for the kernel headers (ie linux-headers-rockchip64 on some RockChip-based Armbian builds)

## Usage

This is used to build a four-node, single-disk Gluster cluster. It has been used on four ROCK64 devices hooked up with USB-SATA devices. While limited, this is a decent setup to test Gluster.

## Parts List

These are the parts I tested this on

- 4x ROCK64 by PINE64 (4 GB RAM, 4-core aarch64 CPU)

- 4x Sabrent USB-SATA adapters with UAS capabilites

- 4x Samsung 256 GB SSDs
