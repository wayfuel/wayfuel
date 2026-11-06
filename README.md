# WayFuel ⛽

**WayFuel** is an open-source route optimization engine designed to identify the optimal fuel stop along a planned road trip across Europe, then inject it directly into **Waze** or **Google Maps**.

Instead of running a basic radial search around the vehicle's current position—which frequently suggests stations in the opposite direction or requires costly highway exits—WayFuel analyzes the actual travel corridor to determine if an off-route stop is mathematically worth the detour.

---

## 🎯 The Problem & The Formula

Standard fuel apps rank stations purely by pump price, ignoring detour friction. A station that is €0.06/L cheaper is a net loss if reaching it adds a 14 km round trip off the highway.

WayFuel computes the **Total Detour Benefit (TDB)**:

$$\text{TDB} = (\Delta\text{Price} \times V_{\text{refuel}}) - (D_{\text{detour}} \times C_{\text{km}}) - T_{\text{cost}}$$

Where:
- $\Delta\text{Price}$: Price difference per liter between the on-route default and the candidate station
- $V_{\text{refuel}}$: Estimated liters to refuel
- $D_{\text{detour}}$: Real-world additional round-trip distance
- $C_{\text{km}}$: Effective cost per kilometer (fuel consumption + wear)
- $T_{\text{cost}}$: Normalized time penalty coefficient (user-defined or route-critical)

If $\text{TDB} \le 0$, the detour is rejected.

---

## 🧭 Optimization Modes

WayFuel supports three distinct routing profiles:

1. **Economical Stop**: Maximizes raw wallet savings by finding the absolute break-even point between detour distance, fuel consumed to reach the station, and pump pricing.
2. **Fastest Stop**: Focuses on immediate corridor continuity. Selects stations located directly along the main trajectory or at immediate off-ramp points with minimal signal delays.
3. **Eco-Responsible Stop**: Minimizes supplementary CO₂ emissions by preventing redundant mileage and high-gradient climbs, with architecture designed to incorporate EV high-power charging corridors.

---

## 📄 License

This project is licensed under the [AGPL-3.0 License](LICENSE) — see the [LICENSE](LICENSE) file for details.
