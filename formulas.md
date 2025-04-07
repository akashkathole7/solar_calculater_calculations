# Solar Calculation Formulas

This document provides detailed information about the mathematical formulas and calculations used in the Solar Ark application for determining solar system sizing, energy generation, financial benefits, and environmental impact.

## System Sizing Formulas

### System Size Calculation

The system size (in kW) is calculated based on the monthly electricity bill:

```
system_size = monthly_consumption / (30 * solar_peak_hours * efficiency)
```

Where:
- `monthly_consumption` = monthly_bill / tariff_rate (in kWh)
- `solar_peak_hours` = average daily peak sun hours in the region (default: 5 hours)
- `efficiency` = system efficiency accounting for losses (default: 0.85 or 85%)

### Required Roof Area

The roof area required for a solar installation is calculated as:

```
area_required = system_size * area_factor
```

Where:
- `area_factor` = area required per kW of solar capacity (default: 10 square meters)
- This may be adjusted based on panel efficiency: `area_factor = standard_area_factor * (0.2 / avg_efficiency)`

## Energy Generation Formulas

### Daily Energy Generation

```
daily_generation = system_size * solar_irradiance * efficiency
```

Where:
- `solar_irradiance` = location-specific daily peak sun hours (varies by district)
- `efficiency` = system efficiency (default: 0.85)

### Monthly Energy Generation

```
monthly_generation = daily_generation * 30
```

### Annual Energy Generation

```
annual_generation = daily_generation * 365
```

## Financial Calculations

### Monthly Savings

```
monthly_gross_savings = monthly_generation * tariff_rate
monthly_net_savings = monthly_gross_savings - monthly_meter_charges
```

Where:
- `tariff_rate` = electricity tariff rate per kWh (varies by district)
- `monthly_meter_charges` = fixed charges for meter, connection, etc. (default: ₹150)

### Annual Savings

```
annual_savings = monthly_net_savings * 12
```

### Lifetime Savings (25 years)

```
lifetime_savings = annual_savings * system_lifespan
```

Where:
- `system_lifespan` = expected lifespan of solar panels (default: 25 years)

## ROI Calculations

### System Cost

```
system_cost = system_size * cost_per_kW * technology_cost_factor
```

Where:
- `cost_per_kW` = standard cost per kW of solar installation (default: ₹45,000)
- `technology_cost_factor` = multiplier based on chosen technology (ranges from 0.8 to 1.8)

### Government Subsidy

Subsidy is determined based on system size:
- For system_size ≤ 1 kW: subsidy = ₹30,000
- For 1 kW < system_size ≤ 2 kW: subsidy = ₹60,000
- For system_size > 2 kW: subsidy = ₹78,000

### Net Cost After Subsidy

```
net_cost = system_cost - subsidy
```

### Payback Period

```
payback_period = net_cost / annual_savings
```

### ROI Percentage

```
roi_percentage = ((lifetime_savings - net_cost) / net_cost) * 100
```

## Environmental Impact Calculations

### CO2 Emissions Reduction

```
annual_co2_savings_kg = annual_generation * co2_emission_factor
annual_co2_savings_tons = annual_co2_savings_kg / 1000
lifetime_co2_savings_tons = annual_co2_savings_tons * system_lifespan
```

Where:
- `co2_emission_factor` = kg of CO2 emissions per kWh of electricity (default: 0.85 kg/kWh)

### Equivalent Trees Planted

```
annual_trees_equivalent = annual_co2_savings_kg / tree_absorption_rate
lifetime_trees_equivalent = annual_trees_equivalent * system_lifespan
```

Where:
- `tree_absorption_rate` = average annual CO2 absorption per tree (default: 21 kg/year)

## Power Generation Percentage

This calculates what percentage of a customer's electricity needs will be covered by solar:

```
power_generation_percentage = (monthly_generation / monthly_consumption) * 100
```

The percentage is capped at 100% for cases where generation exceeds consumption.

## District-Specific Parameters

The application uses district-specific data to provide more accurate calculations:

| District    | Solar Irradiance | Tariff Rate (₹/kWh) |
|-------------|------------------|---------------------|
| Mumbai      | 5.2              | 10.5                |
| Pune        | 5.5              | 9.0                 |
| Nagpur      | 5.7              | 8.5                 |
| Nashik      | 5.6              | 8.8                 |
| Aurangabad  | 5.8              | 8.3                 |
| Thane       | 5.3              | 9.8                 |
| Solapur     | 5.9              | 8.0                 |

## Technology-Specific Parameters

Different solar technologies have varying efficiency and cost factors:

| Technology      | Efficiency | Cost Factor |
|-----------------|------------|-------------|
| Monobifacial    | 19-22%     | 1.2         |
| Polycrystalline | 15-17%     | 0.8         |
| Monocrystalline | 18-22%     | 1.0         |
| Thin-film       | 10-12%     | 0.9         |
| Transparent     | 5-10%      | 1.5         |
| Solar Tiles     | 15-20%     | 1.8         |
| TOPCon          | 21-23%     | 1.3         |
| Perovskite      | 20-25%     | 1.1         |

## Default Constants

The application uses the following default constants for calculations:

- Standard efficiency: 85%
- Solar peak hours: 5 hours/day
- Area required per kW: 10 square meters
- Default tariff rate: 9 ₹/kWh
- Monthly meter charges: ₹150
- System lifespan: 25 years
- CO2 emission factor: 0.85 kg/kWh
- Tree absorption rate: 21 kg CO2/year
- System cost per kW: ₹45,000

These formulas and parameters are implemented in the `SolarCalculator` class and used throughout the application to provide accurate and location-specific solar calculations.