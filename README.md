# AWX + NetBox Starter

Estrutura para rodar playbooks de rede no AWX com inventário vindo do NetBox.

## Passos rápidos no AWX
1. **Execution Environment**: `quay.io/ansible/network-ee:latest`
2. **Project**: aponte para este repositório (Git) ou faça upload manual (tipo Manual).
3. **Inventory** → **Source** (Sourced from a Project): use `inventories/netbox.yml`
   - Em **Environment Variables** do Source, defina `NETBOX_TOKEN` com o token do seu NetBox.
4. **Credentials**: crie **Machine/Network (SSH)** para os switches/roteadores.
5. **Job Template**: selecione o Project, Inventory e um playbook (`playbooks/test_ping.yml` ou `playbooks/ntp_config.yml`).
6. No **NetBox**, garanta:
   - Device com **Primary IP**;
   - **Platform** coerente (`community.network.comware`, `cisco.ios.ios`, `arista.eos.eos`, `junipernetworks.junos.junos`);
   - Tag `para-configurar` (o Source filtra por ela).
   - (Opcional) Custom Field `cf_ansible_network_os` para sobrepor o platform.

## Mapeamento de `ansible_network_os`
- Comware (H3C/HPE): `community.network.comware`
- Cisco IOS: `cisco.ios.ios`
- Arista EOS: `arista.eos.eos`
- Juniper Junos: `junipernetworks.junos.junos`

## Observação
Usando o **network-ee**, as coleções já vêm na imagem, então não é necessário `ansible-galaxy install` durante o job.
