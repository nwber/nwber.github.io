# Cheap compute options

## A catalogue of dirt cheap compute available, for those that want that sort of thing

I was looking for an instance to run things and spend as little money as possible. This is a basic overview of specs for each provider's cheapest instance. The best option, tragically, is OCI's free tier.

Table created with the help of https://www.tablesgenerator.com/markdown_tables

| Provider     | Instance name        | $ / mo | vCPU | RAM (GB) | Storage (GB) | Network I/O (Gbps) | Included egress | Notes                                        |
|--------------|----------------------|--------|------|----------|--------------|--------------------|-----------------|----------------------------------------------|
| Linode       | Nanode 1 GB          | 5      | 1    | 1        | 25           | 40/1               | 1TB             |                                              |
| DigitalOcean | Regular droplets     | 4      | 1    | 0.5      | 10           | ?                  | 0.5TB           |                                              |
| Hetzner      | CPX11 (US)           | 5.59   | 2    | 2        | 40           | ?                  | 1TB             | With IPv4 address                            |
| OVH          | d2-2                 | 6.57   | 1    | 2        | 25           | 0.1/0.1            | ?               |                                              |
| Oracle       | VM.Standard.A1.Flex  | 0      | 4    | 24       | 200          | 1/1                | ?               | Unfortunately, Oracle Cloud is run by Oracle |
| AWS          | t4g.nano (us-east-1) | 3.07   | 2    | 0.5      | 30           | 5 (up to)          | ?               | ARM, and burst-able instance type            |
| Azure        | b1ls                 | 3.80   | 1    | 0.5      | 4            | ?                  | ?               |                                              |

## Value proposition

Does not include Oracle 

## CPU 

| Provider     | Instance name        | $ / mo | vCPU | $ / CPU |
|--------------|----------------------|--------|------|---------|
| AWS          | t4g.nano (us-east-1) | 3.07   | 2    | 1.535   |
| Hetzner      | CPX11 (US)           | 5.59   | 2    | 2.795   |
| Azure        | b1ls                 | 3.80   | 1    | 3.80    |
| DigitalOcean | Regular droplets     | 4      | 1    | 4.00    |
| Linode       | Nanode 1 GB          | 5      | 1    | 5.00    |
| OVH          | d2-2                 | 6.57   | 1    | 6.57    |

## RAM

| Provider     | Instance name        | $ / mo | RAM (GB) | $ / RAM |
|--------------|----------------------|--------|----------|---------|
| Hetzner      | CPX11 (US)           | 5.59   | 2        | 2.795   |
| OVH          | d2-2                 | 6.57   | 2        | 3.285   |
| AWS          | t4g.nano (us-east-1) | 3.07   | 0.5      | 6.14    |
| Linode       | Nanode 1 GB          | 5      | 1        | 5       |
| DigitalOcean | Basic Regular 512MB  | 4      | 0.5      | 8       |
| OVH          | d2-2                 | 6.57   | 2        | 3.285   |
| Azure        | b1ls                 | 6.14   | 0.5      | 12.28   |

## Conclusion

Everyone on Twitter was right! Hetzner rocks. 
