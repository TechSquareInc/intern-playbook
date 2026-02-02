# Power and Cooling Basics for HPC Systems

This section gives quick, practical rules of thumb for early stage planning, estimating electrical power and cooling needs for servers and HPC racks.

## Power Sizing
When installing HPC systems, it's important to address whether the electrical infrastructure can safely support the hardware under a worst-case-scenario compute load. Underestimating power is a fast way to cause outages or system failures. There is a core formula to for estimating electrical power which balances the fundamental relationship between amps, watts, and voltage.

### Core Formula

**Current (Amps) = Power (Watts) ÷ Voltage (Volts)**

For example, a 2200-watt system on operating 220-volt power will draw approximately 10 amps at full load. Power sizing calculations should always assume peak draw rather than idle or average usage.

### Common Reference Points
|Power|Voltage|Current |
|-----|-------|--------|
|1200W|120V   |   ~10A |
|2000W|208-220V|~9-10A |
|3000W|220-240V|~12-14A|

### Rack Level Planning
Server power draw varies by workload, but infrastructure must support worst-case draw, and should be limited to 80% of breaker capacity. For a rack with multiple systems, you could have ten 2200-watt servers all operating on 220-volt power. 22,000 watts ÷ 220-volts is approximately 100 amps total. This is why HPC racks often have multiple PDUs to distribute power evenly, allowing for redundancy if one fails. They also implement multi-phase power to balance loads across multiple conductors, allowing large racks to draw high total power safely and reducing the risk of tripping circuits.

## Cooling Sizing
In data centers, every watt consumed becomes heat, which means cooling design is inseperable from power design. With a 2200-watt server, we can follow a basic conversion of Watt to BTU/hr. 1 Watt = 3.412 BTU/hr. 2200-W x 3.412 = 7,500 BTU/hr. This represents the minimum cooling capacity required to remove the generated heat. For early planning, engineers often use simplified multipliers: Cooling(BTU/hr) = Power(Watts) x 3-10. This wide range allows for airflow loss, hot/cold air mixing, fan inefficiencies, and a general safety margin. The 10x multiplier is intentionally conservative and commonly used during preliminary sizing to slightly overprovision cooling, which is often perferred in HPC environments.

### Rack Cooling Example
A few high density racks can consume as much cooling as an entire small server room. Take 1 rack at 20 kW load. 20,000-W x 3.412 = ~68,000 BTU/hr. This equates roughly to 5-6 tons of cooling for a single rack.
