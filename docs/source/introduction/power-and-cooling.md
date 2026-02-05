# Power and Cooling Basics for HPC Systems

This section provides practical guidance for understanding how electrical power is distributed, protected, and planned in an HPC environment. It explains how PDUs, phases, breakers, and redundancy work together, and how power consumption directly drives cooling requirements. These guidelines are intended for early stage planning, as well as operational awareness, estimating electrical power and cooling needs for servers and HPC racks.

## Electrical Power Fundamentals
Electrical load planning is based on the fundamental relationship between power, voltage, and current. Current draw is calcualted by dividing power by voltage and should assume worst-case or peak load rather than average or idle usage. When installing HPC systems, it's important to address whether the electrical infrastructure can safely support the hardware under a worst-case-scenario compute load. Underestimating power is a fast way to cause outages or system failures.

### Core Formula

**Current (Amps) = Power (Watts) ÷ Voltage (Volts)**

#### Common Reference Points
|Power|Voltage|Current |
|-----|-------|--------|
|1200W|120V   |   ~10A |
|2000W|208-220V|~9-10A |
|3000W|220-240V|~12-14A|

For example, a 2200-watt system on operating 220-volt power will draw approximately 10 amps at full load. As total rack density increases, these individual draws quickly add up, which is why careful power distribution and conservative limits are essential in HPC environments.

## Rack Level Power Sizing
Server power draw varies by workload, but infrastructure must support worst-case draw, and should be limited to 80% of breaker capacity. For a rack with multiple systems, you could have ten 2200-watt servers all operating on 220-volt power. 22,000 watts ÷ 220-volts is approximately 100 amps total. This is why HPC racks often have multiple PDUs (Power Distribution Units) to distribute power evenly, allowing for redundancy if one fails. They also implement multi-phase power to balance loads across multiple conductors, allowing large racks to draw high total power safely and reducing the risk of tripping circuits.

### Three-Phase Power and PDU Design
Each PDU is supplied with three electrical phases, commonly referred to as A, B, and C. Each phase is rated for 30 amps. Because these circuits support continuos loads, the 80% rule is applied, meaning sustained current should remain at or below approximately 24 amps per phase.

Power is distributed to each PDU through a bus plug connected to the overhead bus bar above each pod. To provide primary overcurrent protection at the phase level, each bus plug contains a dedicated 30-amp breaker for each phase. These breakers serve as the first layer of protection for the PDU and its downstream components.

Within each PDU, power is further divided into sections of outlets referred to as segments. Each phase feeds two segments, resulting in a toal of six segments per PDU. Each segment represents an independent entry point to its associated phase and is protected by a 20-amp breaker or fuse. Applying the 80% rule at this level means segment loads should ideally remain around 16-amps.

This design creates multiple layers of protection. While segment level breakers protect individual outlet groups, bus plug breakers protect the overall phase feed into the PDU. Together these layers reduce the likelihood of widespread outages and allow faults to be isolated without impacting the entire rack or pod.

### Rack Level Power Distribution and Redundancy
Racks are generally evaluated as if only one side of their power infrastructure is active. One PDU and its associated bus are considered the primary power path, while the opposing PDU is treated as redundant. When loads are evenly balanced across both PDUs and across all three phases, no individual breaker should approach its continuous load limit. With this configuration, the loss of one power side should not result in service disruption. The redundant side is expected to absorb the full load without exceeding breaker thresholds.

## Cooling Sizing
In data centers, every watt consumed becomes heat, which means cooling design is inseperable from power design. With a 2200-watt server, we can follow a basic conversion of Watt to BTU/hr. 1 Watt = 3.412 BTU/hr. 2200-W x 3.412 = 7,500 BTU/hr. This represents the minimum cooling capacity required to remove the generated heat. For early planning, engineers often use simplified multipliers: Cooling(BTU/hr) = Power(Watts) x 3-10. This wide range allows for airflow loss, hot/cold air mixing, fan inefficiencies, and a general safety margin. The 10x multiplier is intentionally conservative and commonly used during preliminary sizing to slightly overprovision cooling, which is often perferred in HPC environments.

### Rack Cooling Example
A few high density racks can consume as much cooling as an entire small server room. Take 1 rack at 20 kW load. 20,000-W x 3.412 = ~68,000 BTU/hr. This equates roughly to 5-6 tons of cooling for a single rack.

---
## Resources
- [Ohm's Law](http://hyperphysics.phy-astr.gsu.edu/hbase/electric/ohmlaw.html): The physics formula electrical load planning directly derives from.
- [Ten Simple Rules for Building and Maintaining Sustainable High-Performance Computing Infrastructure](https://pmc.ncbi.nlm.nih.gov/articles/PMC12453185/): Ten practical rules for building sustainable power solutions in resource-limited settings.
- [Energy Efficieny Trends in HPC](https://arxiv.org/html/2503.17283v1): Practical advice on how to analyze and optimize applications to reduce their energy consumption without compromising on performance.
