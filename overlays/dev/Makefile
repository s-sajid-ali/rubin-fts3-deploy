get-secrets:
	mkdir -p fts3/etc/.secrets
	vault kv get --field=hostcert.pem secret/rubin/usdf-fts3-dev/fts3  > fts3/etc/.secrets/fts3-hostcert.pem
	vault kv get --field=hostkey.pem secret/rubin/usdf-fts3-dev/fts3  > fts3/etc/.secrets/fts3-hostkey.pem
	vault kv get --field=usdf-fts3db-fts3-password secret/rubin/usdf-fts3-dev/fts3db  > fts3/etc/.secrets/fts3db-fts3-password
	vault kv get --field=usdf-fts3db-username secret/rubin/usdf-fts3-dev/fts3db  > fts3/etc/.secrets/fts3db-username
	vault kv get --field=usdf-fts3db-fts3connstr secret/rubin/usdf-fts3-dev/fts3db  > fts3/etc/.secrets/fts3db-fts3connstr
	mkdir -p mariadb/etc/.secrets
	vault kv get --field=usdf-fts3db-root-password secret/rubin/usdf-fts3-dev/fts3db  > mariadb/etc/.secrets/fts3db-root-password
	vault kv get --field=usdf-fts3db-fts3-password secret/rubin/usdf-fts3-dev/fts3db  > mariadb/etc/.secrets/fts3db-fts3-password
	vault kv get --field=usdf-fts3db-username secret/rubin/usdf-fts3-dev/fts3db  > mariadb/etc/.secrets/fts3db-username

clean-secrets:
	rm -rf fts3/etc/.secrets mariadb/etc/.secrets

run-dump: 
	kubectl kustomize .

dump: get-secrets run-dump clean-secrets

run-apply:  
	kubectl apply -k .

apply: get-secrets run-apply clean-secrets

#run-destroy:
#	kubectl delete -k .

#destroy: get-secrets rucio run-destroy clean-secrets


