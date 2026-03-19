# Oracle Cloud Free Tier

**Account:** Active — US East (Ashburn) region

**VCN:** Manitec-vcn ✅

## Current Instance

- **Shape:** VM.Standard.E2.1.Micro (AMD)
- **Specs:** 1 OCPU / 1GB RAM / 0.48 Gbps
- **Public IP:** 129.158.244.106
- **Username:** ubuntu
- **Status:** Running

## Goal Instance (Not Yet Obtained)

- **Shape:** VM.Standard.A1.Flex (Ampere ARM)
- **Specs:** Up to 4 OCPU / 24GB RAM — Always Free
- **Issue:** Out of capacity — extremely high demand
- **Workarounds:** PAYG upgrade for priority access, or [hitrov/oci-arm-host-capacity](https://github.com/hitrov/oci-arm-host-capacity) auto-retry script

## Planned Use

**Luanti (formerly Minetest) game server**

- Default port: UDP 30000
- Need to open port in Security List
- Add 2GB swap file on micro instance if using E2.1.Micro
- Install headless, keep world/mods light on 1GB RAM

## Always Free Resources

- 2x AMD Micro instances (1 OCPU / 1GB each)
- 1x Ampere A1 (up to 4 OCPU / 24GB total)
- 200GB block storage
- Never expires
