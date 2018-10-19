How to:


Les nodes UCPs et DTRs sont en HA
Les installations des UCP et DTR sont fait en offline avec la doc officiel.

Les playbooks sont disponible pour pousser les images et ajouter les workers.
Les managers et dtr doitvent etres installés mannuellement. (TODO les playbookspour automatisers)

pour deployer les images sur des workers
	dtr:
		ajouter le nodes dans dtr-nodes dans  le fichier hosts et executer le playbooks docker-dtr-play.yml
			"ansible-playbook -i hosts docker-dtr-play.yml"

	ucp:
		ajouter le nodes dans new-workers dans  le fichier hosts et executer le playbooks docker-ucp-play.yml
			"ansible-playbook -i hosts docker-ucp-play.yml"
		
		

ajouter le nodes dans new-nodes dans  le fichier hosts et executer le playbooks swarm-worker-join.yml
	"ansible-playbook -i hosts swarm-worker-join.yml"
		/!\ il faut ajouter les nodes un par un. (TODO ameliorer les roles pour ajouter plusieurs nodes à la fois)
		une fois le playbook terminé déplacer le node dans worker-nodes

TODO:
	ajouter load balancer pour les UCPs et DTRs, nom de dns, mettre à jours les nouveaux certificats.
	modifier le ficher hosts avec le nouveau ip du load balancer du ucp 'lb_ucp_manager'
	modifier le vars "lb_ucp_manager" dans le playbook swarm-worker-join.yml







Nodes List:
===========

[ucp-lb]
lb_ucp_manager ansible_ssh_host=192.32.75.40 ansible_ssh_port=22 ansible_ssh_user=root

[ucp-masters]
192.32.75.40
192.32.75.136
192.32.75.137

[dtr-nodes]
192.32.75.41
192.32.75.138
192.32.75.139

[worker-nodes]
192.32.75.20 ansible_ssh_port=22 ansible_ssh_user=szrafi
192.32.75.140
192.32.75.45

[new-worker]
