all: install

.PHONY: disable enable install start stop uninstall

install:
	stat mnt-disk > /dev/null 2>&1 || (echo "mnt-disk file not found" ; exit 1)
	stat mnt-units.service > /dev/null 2>&1 || (echo "mnt-units.service file not found" ; exit 1)
	mkdir -p /etc/ephemeral-scripts/
	cp mnt-resource_start /etc/ephemeral-scripts/
	chmod 750 /etc/ephemeral-scripts/mnt-resource_start
	cp mnt-resource_stop /etc/ephemeral-scripts/
	chmod 750 /etc/ephemeral-scripts/mnt-resource_stop
	cp mnt-disk.service /etc/systemd/system/
	cp mnt-resource.mount /etc/systemd/system/
	cp mnt-units.service /etc/systemd/system/
	cp mnt-disk /etc/default/
	systemctl daemon-reload

uninstall:
	rm -f /etc/ephemeral-scripts/mnt-resource_start
	rm -f /etc/ephemeral-scripts/mnt-resource_stop
	rmdir /etc/ephemeral-scripts/
	rm -f /etc/systemd/system/mnt-disk.service
	rm -f /etc/systemd/system/mnt-resource.mount
	rm -f /etc/systemd/system/mnt-units.service
	rm -f /etc/default/mnt-disk
	systemctl daemon-reload

enable:
	systemctl enable mnt-disk.service
	systemctl enable mnt-resource.mount
	systemctl enable mnt-units.service

disable:
	systemctl disable mnt-units.service
	systemctl disable mnt-resource.mount
	systemctl disable mnt-disk.service

start:
	systemctl start mnt-disk.service
	systemctl start mnt-resource.mount
	systemctl start mnt-units.service

stop:
	systemctl stop mnt-units.service
	systemctl stop mnt-resource.mount
	systemctl stop mnt-units.service
