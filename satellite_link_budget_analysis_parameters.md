# Satellite Communication Link Budget Analysis: Parameters, Equations, and Engineering Considerations

## 1. Definition of a Link

In telecommunications, a **link** is a communication path through which
information travels from a transmitting system to a receiving system. A
link includes the transmitter, transmitting antenna, propagation path,
receiving antenna, receiver, and the relevant signal-processing
functions.

In a satellite communication system, a link may connect a satellite to a
ground station, a ground station to a satellite, or two satellites to
each other.

-   **Downlink:** communication from the satellite to a ground station.
-   **Uplink:** communication from a ground station to the satellite.
-   **Crosslink / inter-satellite link (ISL):** communication between
    satellites.
-   **Forward link:** commonly used for the direction from a network or
    hub toward a user terminal.
-   **Return link:** commonly used for the direction from a user
    terminal toward a network or hub. Exact usage depends on the system.

A link is not simply the presence of a radio signal. It must deliver
information with adequate signal quality, error performance,
availability, and data rate under the conditions expected during
operation.

## 2. What Is Link Budget Analysis?

**Link budget analysis** is the accounting of gains and losses
experienced by a signal as it travels from a transmitter to a receiver.
It estimates received power and determines whether the link can meet the
required communication performance.

A link budget is usually calculated in decibels so that gains can be
added and losses subtracted. It can be used to evaluate whether a
proposed combination of transmitter power, antennas, frequency,
distance, receiver performance, bandwidth, and modulation is sufficient.

A complete analysis should answer questions such as:

-   Will the receiver receive enough signal power?
-   Is the received signal strong enough relative to noise and
    interference?
-   Can the selected modulation and coding scheme support the required
    bit error rate?
-   What is the link margin under nominal and worst-case conditions?
-   How will performance change during a satellite pass?
-   What data rate and communication availability can reasonably be
    expected?

A link budget is an engineering estimate based on assumptions. It does
not, by itself, prove that a complete radio system will work; testing,
regulatory compliance, antenna measurements, and implementation
verification are also needed.

## 3. Link Budget Building Blocks

A simplified downlink follows this chain:

1.  Transmitter output power
2.  Transmitter-side losses
3.  Transmitting antenna gain
4.  Propagation losses, including free-space path loss
5.  Receiving antenna gain
6.  Receiver-side losses
7.  Received carrier power
8.  Noise and interference assessment
9.  Demodulation and decoding requirement
10. Link margin

For a basic power budget:

$$
P_r = P_t + G_t - L_t - L_{path} + G_r - L_r
$$

All terms in this equation are in dB-based units: power terms in dBW or
dBm, and gains/losses in dB or dBi. The equation is only valid when
units and reference points are consistent and each gain or loss is
counted exactly once.

## 4. Essential Units and Decibel Mathematics

### 4.1 Watt (W)

The watt is the SI unit of power. RF transmitter output power may be
specified in watts or milliwatts.

### 4.2 Decibel (dB)

A decibel expresses a ratio between two power levels:

$$
G_{dB} = 10\log_{10}\left(\frac{P_2}{P_1}\right)
$$

For voltage ratios, the formula is $20\log_{10}(V_2/V_1)$ only
when the compared voltages use the same impedance.

A positive dB value represents a gain or increase in the ratio; a
negative value represents a reduction.

### 4.3 dBW

dBW expresses power relative to 1 watt:

$$
P_{dBW} = 10\log_{10}(P_W)
$$

Conversion back to watts:

$$
P_W = 10^{P_{dBW}/10}
$$

Examples: - 1 W = 0 dBW - 10 W = 10 dBW - 0.1 W = -10 dBW

### 4.4 dBm

dBm expresses power relative to 1 milliwatt:

$$
P_{dBm} = 10\log_{10}(P_{mW})
$$

Conversions: - (P\_{dBm}=P\_{dBW}+30) - (P\_{dBW}=P\_{dBm}-30)

### 4.5 dBi

dBi expresses antenna gain relative to an ideal isotropic radiator. It
is commonly used for satellite and ground-station antenna gain.

### 4.6 dBd

dBd expresses antenna gain relative to a half-wave dipole. For a
standard reference dipole, dBi is approximately dBd + 2.15 dB. Check the
antenna specification to identify which reference is used.

### 4.7 dB-Hz

dB-Hz is used for carrier-to-noise-density ratio, (C/N_0). It describes
carrier power relative to noise power spectral density, rather than
relative to noise integrated over a specified bandwidth.

### 4.8 Rules for adding and subtracting

When a link budget is expressed in decibels: - Add power gains. -
Subtract losses. - Keep absolute power in dBW or dBm. - Do not add dBW
directly to dBm without conversion. - Avoid counting the same loss
twice. - Clearly document each term's reference point.

## 5. Transmitter Parameters

### 5.1 Transmitter output power, (P_t)

The RF power delivered by the transmitter at a specified reference
point, usually the radio output connector.

Common units are W, dBW, and dBm.

Why it matters: increasing transmitter power raises the transmitted
signal level, but may increase electrical power consumption, heat, mass,
and battery demand. The selected power must be consistent with the radio
design, power budget, duty cycle, and regulatory limits.

Example conversion:

$$
P_{t,dBW} = 10\log_{10}(P_{t,W})
$$

### 5.2 Transmitter duty cycle

The fraction of time the transmitter is active. It affects average
energy consumption and thermal behaviour. Link budgets normally use the
RF power during transmission, while spacecraft power budgets must
account for average consumption and duty cycle.

### 5.3 Transmitter-side feeder and connector loss, (L_t)

Power lost between the transmitter output and antenna feed point due to
coaxial cable, waveguides, connectors, filters, switches, matching
networks, or other components.

Expressed in dB. Include only losses that lie between the chosen
transmitter power reference point and the antenna reference point.

### 5.4 Transmit antenna gain, (G_t)

The directional gain of the transmitting antenna in the direction of the
receiver, expressed in dBi.

Antenna gain depends on frequency, direction, polarization, and antenna
configuration. A nominal peak gain should not automatically be used if
the antenna is not pointing in that direction.

### 5.5 Effective isotropic radiated power (EIRP)

EIRP represents the power that an ideal isotropic antenna would need to
radiate to produce the same power density in the direction of interest.

$$
EIRP_{dBW} = P_{t,dBW} - L_{t,dB} + G_{t,dBi}
$$

EIRP is useful for comparing transmitting systems. It is directional and
depends on the antenna gain in the relevant direction.

## 6. Frequency, Wavelength, and Bandwidth

### 6.1 Operating frequency, (f)

The carrier frequency of the radio signal, measured in Hz, kHz, MHz, or
GHz.

Frequency affects: - Free-space path loss for a fixed distance and
isotropic transmit/receive antenna gains. - Antenna dimensions and
achievable gain. - Atmospheric and rain attenuation, which become more
important in many higher-frequency links. - Regulatory allocations,
antenna design, propagation, Doppler shift, and hardware availability.

Higher frequency does not automatically mean a worse complete link:
antenna gain, antenna size, bandwidth, and system design also matter.

### 6.2 Wavelength, ($\lambda$)

The wavelength is the physical distance travelled by one cycle of the
wave:

$$
\lambda = \frac{c}{f}
$$

where (c) is the speed of light in vacuum, approximately
$3.00\times10^8$ m/s.

Frequency must be in Hz to obtain wavelength in metres.

### 6.3 Bandwidth, (B)

Bandwidth is the frequency range occupied by or available to a signal,
measured in Hz. Distinguish among: - Allocated channel bandwidth -
Occupied signal bandwidth - Receiver noise bandwidth - Sampling or
processing bandwidth

These are related but not always identical. Receiver noise calculations
should use the appropriate effective noise bandwidth, not automatically
the allocated channel bandwidth.

### 6.4 Bit rate, (R_b)

The number of information-channel bits transmitted per second, in bit/s.
Depending on convention, the stated rate may refer to uncoded
information bits or coded bits. Make the convention explicit.

A higher bit rate generally requires more received energy per second to
maintain the same energy per bit, unless other parameters change.

### 6.5 Symbol rate, (R_s)

The number of modulation symbols transmitted per second, in symbols/s or
baud.

For an uncoded modulation with (m) bits per symbol:

$$
R_b = R_s\log_2(m)
$$

This simple relation needs adjustment when coding, framing, pilots, or
overhead are included. For example, BPSK carries one coded bit per
symbol, while QPSK carries two coded bits per symbol.

## 7. Propagation Distance and Orbital Geometry

### 7.1 Slant range, (d)

The straight-line distance between the satellite and the ground station
at a given time. It is not generally equal to the satellite's altitude.

Slant range changes throughout a satellite pass: - It is shortest near
the point of closest approach, often near maximum elevation. - It
increases toward acquisition and loss of signal. - The maximum range for
the pass depends on the minimum elevation angle used.

Use slant range in the free-space path loss equation.

### 7.2 Satellite altitude

The satellite's height above the reference Earth surface. Altitude alone
is insufficient to calculate instantaneous range unless orbital position
and ground-station geometry are also known.

### 7.3 Elevation angle

The angle between the satellite direction and the local horizontal plane
at the ground station. A higher elevation angle often corresponds to a
shorter path through the atmosphere and a more favourable antenna view.
The lowest permitted elevation may be limited by terrain, obstructions,
antenna tracking, interference, or mission rules.

### 7.4 Line of sight (LOS)

A direct, unobstructed radio path between the transmitting and receiving
antennas. Earth blockage prevents communication when the satellite is
below the ground station's horizon. Local buildings, terrain,
vegetation, and structures can also obstruct the path.

### 7.5 Free-space path loss (FSPL)

FSPL represents the reduction in received power density due to geometric
spreading of a radio wave in free space. It is not energy absorbed by
the vacuum.

A commonly used form is:

$$
FSPL_{dB} = 32.44 + 20\log_{10}(f_{MHz}) + 20\log_{10}(d_{km})
$$

This constant is appropriate when frequency is in MHz and distance is in
km. Equivalent forms use different constants for different units, such
as GHz and km.

The fundamental expression is:

$$
FSPL = 20\log_{10}\left(\frac{4\pi d}{\lambda}\right)
$$

Assumptions include far-field propagation and an ideal free-space path.
Real links may have additional losses. FSPL increases by about 6 dB when
distance doubles, at a fixed frequency. It also increases by about 6 dB
when frequency doubles, at a fixed distance, when comparing isotropic
antenna reference gains.

## 8. Antenna Parameters

### 8.1 Antenna gain

Gain describes how strongly an antenna concentrates radiation in a
direction compared with a reference antenna. For link budgets, use the
gain in the actual direction of the other endpoint, not necessarily the
peak gain.

### 8.2 Antenna radiation pattern

A diagram or function describing antenna gain versus direction. It
includes the main lobe, side lobes, and possibly nulls. Radiation
pattern matters when the satellite rotates, a deployable antenna changes
orientation, or a ground station tracks the satellite.

### 8.3 Antenna pointing loss

Loss caused by misalignment between the antenna's direction of maximum
gain and the direction of the other endpoint. The value depends on
antenna beamwidth, pointing error, and the antenna pattern.

### 8.4 Polarization mismatch loss

Loss when the transmitted and received wave polarizations do not match.
Possible polarizations include linear, circular, and elliptical.
Satellite attitude changes and ground-station orientation can affect
polarization alignment.

### 8.5 Antenna efficiency

The fraction of input power converted into radiation, accounting for
relevant losses. Efficiency affects realized antenna gain. Avoid
separately subtracting efficiency loss if the antenna specification
already provides realized gain that includes it.

### 8.6 Effective aperture

The effective aperture (A_e) relates received power density to available
received power:

$$
A_e = \frac{G_r\lambda^2}{4\pi}
$$

where (G_r) is linear (not dBi) antenna gain. This relationship is
useful for understanding how antenna gain and wavelength affect
reception.

### 8.7 Ground-station antenna gain, (G_r)

The receive antenna gain in the satellite's direction, expressed in dBi.
It depends on antenna size, frequency, efficiency, pointing, and
radiation pattern.

### 8.8 Antenna tracking

The process of keeping a directional ground antenna pointed toward the
satellite. Tracking error may reduce gain and therefore the link margin.
A small CubeSat antenna may be broad-beam and require little or no
active tracking, whereas a high-gain ground dish usually needs tracking.

## 9. Receiver Parameters

### 9.1 Receiver input power, (P_r)

The RF power available at the defined receiver reference point. Be
explicit about whether the value is measured at the antenna port, after
a cable, or at another point.

### 9.2 Receiver sensitivity

The minimum input signal level at which a receiver meets a specified
performance requirement, such as a given bit error rate, packet error
rate, or signal-to-noise ratio, under stated bandwidth, modulation,
coding, and test conditions.

Sensitivity is not a universal constant for a radio. A quoted value is
meaningful only with its associated operating conditions.

### 9.3 Noise figure, (NF)

Noise figure quantifies how much a component or receiver degrades
signal-to-noise ratio compared with an ideal noiseless component. It is
commonly specified in dB.

The corresponding linear noise factor is:

$$
F = 10^{NF/10}
$$

A lower noise figure generally improves receiver sensitivity, all else
being equal. In systems with a low-noise amplifier near the antenna,
cable losses before that amplifier can be especially damaging.

### 9.4 System noise temperature, (T\_{sys})

The effective noise temperature representing the combined noise
contributions of the antenna, environment, feeder, amplifier, and
receiver, referred to a defined point in the system. It is measured in
kelvin.

System noise temperature is often used for satellite and radio astronomy
receiver analyses. Be careful to use a consistent reference plane and
include the relevant antenna and receiver contributions.

### 9.5 Thermal noise power

Thermal noise in a bandwidth (B) is described by:

$$
N = kTB
$$

where: - $k=1.380649\times10^{-23}$ J/K is Boltzmann's
constant - (T) is the effective noise temperature in kelvin - (B) is the
effective noise bandwidth in Hz

In dBW:

$$
N_{dBW} = 10\log_{10}(kTB)
$$

At approximately 290 K, a common reference temperature, the thermal
noise density is approximately -174 dBm/Hz. Therefore:

$$
N_{dBm} \approx -174 + 10\log_{10}(B_{Hz})
$$

This approximation describes thermal noise at the stated reference
temperature; receiver noise figure or system noise temperature must also
be accounted for where applicable.

### 9.6 Low-noise amplifier (LNA)

An LNA amplifies a weak received signal while adding as little noise as
practical. Its gain and noise figure affect the receiver chain. The
LNA's location matters because losses before the LNA can significantly
worsen overall system noise performance.

### 9.7 Receiver bandwidth

The effective bandwidth over which receiver noise is integrated. A wider
bandwidth generally admits more noise power. It must be sufficient for
the selected waveform and filtering but should not be assumed to equal
the bit rate.

## 10. Signal-to-Noise and Digital Link Quality

### 10.1 Carrier-to-noise ratio, (C/N)

The ratio of carrier power (C) to noise power (N) measured over a
defined bandwidth:

$$
(C/N)_{dB} = C_{dBW} - N_{dBW}
$$

The bandwidth and measurement reference must be specified.

### 10.2 Carrier-to-noise-density ratio, (C/N_0)

The carrier power divided by noise power spectral density, typically
expressed in dB-Hz:

$$
(C/N_0)_{dB-Hz} = C_{dBW} - N_{0,dBW/Hz}
$$

It allows comparisons independent of a particular noise bandwidth,
provided the carrier and noise-density reference points are consistent.

### 10.3 Energy per bit to noise spectral density ratio, (E_b/N_0)

(E_b/N_0) measures received energy per bit relative to noise spectral
density. It is commonly used to evaluate digital modulation and coding
performance.

$$
(E_b/N_0)_{dB} = (C/N_0)_{dB-Hz} - 10\log_{10}(R_b)
$$

Here, (R_b) must be defined consistently. For a coded link, the required
threshold may be specified relative to information-bit rate or coded-bit
rate depending on the convention and modem documentation.

### 10.4 Required (E_b/N_0)

The minimum (E_b/N_0) required to meet a specified error-rate target for
the chosen modulation, coding, synchronization, and receiver
implementation. Obtain this value from modem documentation, a validated
simulation, or an appropriate theoretical curve. It is not the same for
every modulation or coding scheme.

### 10.5 Bit error rate (BER)

The fraction of received bits that are detected incorrectly. BER
performance depends on modulation, coding, (E_b/N_0), synchronization,
phase and frequency errors, and implementation effects.

### 10.6 Packet error rate (PER) and frame error rate (FER)

The fraction of packets or frames received with errors. These metrics
matter when communication protocols reject corrupted frames or require
retransmission. BER alone may not fully predict application-level
reliability.

### 10.7 Modulation and coding

Modulation maps information to transmitted symbols; coding adds
structured redundancy that can improve error performance. Different
schemes trade off data rate, bandwidth, required signal quality,
processing complexity, and power efficiency.

Examples: - **BPSK:** one coded bit per symbol; often robust for a given
implementation. - **QPSK:** two coded bits per symbol; can increase
spectral efficiency at a comparable symbol rate. - **GMSK:** a
continuous-phase modulation used in some narrowband radio systems. -
**FEC:** forward error correction that can improve reliability at the
cost of redundancy and processing.

Do not assume a fixed required (E_b/N_0) without specifying the
modulation, coding, target error rate, and implementation assumptions.

## 11. Link Margin

### 11.1 Definition

Link margin is the amount by which the calculated link performance
exceeds the minimum required performance.

A simple power-based form is:

$$
M_{dB} = P_{r,dBW} - P_{required,dBW}
$$

This form is appropriate when the required receiver power is a valid
threshold for the specific operating conditions.

For a digital link, a more directly useful form is:

$$
M_{dB} = (E_b/N_0)_{available} - (E_b/N_0)_{required}
$$

The available and required values must use the same definition and
reference.

### 11.2 Interpretation

-   **Positive margin:** calculated performance exceeds the requirement.
-   **Zero margin:** calculated performance exactly meets the
    requirement, leaving no allowance for unmodelled degradation.
-   **Negative margin:** calculated performance falls short of the
    requirement.

A positive margin does not guarantee success if assumptions are wrong or
unmodelled effects are significant. The design margin should be selected
based on mission risk, uncertainty, expected degradation, and required
availability.

### 11.3 Worst-case and nominal margin

A nominal budget uses typical conditions. A worst-case budget evaluates
challenging but credible conditions, such as maximum slant range, low
elevation, minimum transmitter output, antenna pointing error, and
temperature-dependent hardware performance.

## 12. Additional Propagation and Implementation Losses

Include applicable losses, with a clear rationale and without
double-counting.

### 12.1 Atmospheric gas attenuation

Absorption by atmospheric gases, especially oxygen and water vapour, can
attenuate radio signals. Its importance depends on frequency, elevation
angle, weather, and path length through the atmosphere.

### 12.2 Rain attenuation

Rain can absorb and scatter radio energy, particularly at higher
frequencies. It is often a major concern for some microwave and
higher-frequency links, but may be much less significant for typical
VHF/UHF CubeSat links.

### 12.3 Cloud, fog, and other hydrometeor effects

These can contribute to attenuation at relevant frequencies. Include
them when justified by the operating frequency and required
availability.

### 12.4 Ionospheric effects

The ionosphere can cause effects such as Faraday rotation,
scintillation, group delay, and phase changes. Relevance depends on
frequency, geometry, solar conditions, and the radio system.

### 12.5 Multipath and local obstruction

Reflections from the ground, buildings, and nearby objects can cause
fading or interference. Local obstruction may block the direct path
entirely. A clear free-space budget does not automatically account for
these effects.

### 12.6 Polarization, pointing, and deployment losses

These arise from antenna orientation, imperfect pointing, deployment
tolerances, spacecraft attitude, and mechanical or electrical
imperfections. Estimate them from the actual antenna and mission design
rather than assigning arbitrary values.

### 12.7 Implementation loss

A practical allowance for degradation relative to ideal theoretical
performance, potentially including modem imperfections, phase noise,
quantization, filtering, synchronization, and other implementation
effects. Define what is included so the same effect is not included in
multiple budget terms.

### 12.8 Cable, connector, filter, and switch losses

These occur in the RF chain. Use component specifications or
measurements at the relevant frequency and temperature where possible.
Record the reference plane for each loss.

### 12.9 Doppler shift

Relative motion between satellite and ground station changes the
received carrier frequency. For speeds small relative to the speed of
light, the approximate magnitude is:

$$
|\Delta f| \approx f_c\frac{|v_r|}{c}
$$

where (f_c) is carrier frequency and (v_r) is relative radial velocity.
The sign depends on whether the range is increasing or decreasing.

Doppler shift is primarily a frequency-offset issue rather than a direct
power loss. It can impair acquisition, carrier tracking, or demodulation
if the receiver cannot accommodate it. Doppler rate may also matter.

## 13. Uplink and Downlink Differences

### 13.1 Downlink

The satellite transmits and the ground station receives. Satellite
transmit power and antenna constraints may be tight because of
spacecraft mass, volume, energy, and thermal limitations. Ground
stations may use larger antennas and more capable receivers.

### 13.2 Uplink

The ground station transmits and the satellite receives. Ground-station
EIRP may be relatively high, but the satellite receiver antenna gain,
noise figure, spacecraft orientation, and onboard power constraints
still matter.

### 13.3 Separate budgets

Calculate uplink and downlink independently. Their frequencies,
transmitter powers, antenna gains, bandwidths, data rates, receiver
noise figures, modulation, coding, and propagation conditions may
differ. A bidirectional link is constrained by the direction that fails
to meet its performance requirement first.

## 14. Link Availability and Contact Time

### 14.1 Link availability

The proportion of the required operating time during which the link
meets its performance target. Availability can be affected by satellite
visibility, ground-station scheduling, weather, equipment reliability,
interference, and link margin.

### 14.2 Contact or pass duration

The time during which the satellite is visible above a defined elevation
mask. Actual usable communication time may be shorter because of
acquisition, tracking, Doppler settling, protocol overhead, or a minimum
required elevation angle.

### 14.3 Data volume per pass

A first-order estimate is:

$$
	ext{Data volume (bits)} \approx R_{useful}\times t_{usable}
$$

where (R\_{useful}) is the useful application data rate and
(t\_{usable}) is usable contact time. Reduce the estimate for framing,
coding overhead, retransmissions, idle periods, and operational
constraints as appropriate.

### 14.4 Data rate and margin trade-off

Increasing data rate generally reduces (E_b/N_0) for a fixed (C/N_0),
because the available signal energy is spread across more bits per
second. Lower data rates may improve link robustness but increase the
time needed to transfer the same amount of data.

## 15. Other System and Mission Constraints

A technically positive link budget is not sufficient on its own.
Consider the following:

-   **Frequency allocation and licensing:** the operating frequency and
    emission must comply with applicable national and international
    rules.
-   **Power budget:** transmitter, amplifier, and processing power must
    fit spacecraft energy availability and duty-cycle constraints.
-   **Thermal design:** transmitter operation and RF power amplifiers
    generate heat.
-   **Mass and volume:** antenna size, deployment hardware, cabling, and
    radio equipment must fit the spacecraft.
-   **Spacecraft attitude and spin:** antenna direction and polarization
    can vary with spacecraft orientation.
-   **Ground-station location and availability:** latitude, horizon
    obstructions, network access, and scheduling affect contact
    opportunities.
-   **Interference:** other transmitters and adjacent-channel systems
    may degrade reception.
-   **Protocol overhead:** preambles, headers, synchronization, coding,
    and retransmissions reduce useful application throughput.
-   **Regulatory EIRP and spectral limits:** these can constrain
    transmit power, antenna gain, and waveform choices.
-   **Reliability and redundancy:** component failure, reset behaviour,
    and backup communication modes affect mission resilience.

## 16. A General Link Budget Equation

A simplified received-power equation for a one-way link is:

$$
P_{r,dBW} = P_{t,dBW} + G_{t,dBi} - L_{t,dB} - FSPL_{dB} + G_{r,dBi} - L_{r,dB} - L_{other,dB}
$$

where: - (P_t): transmitter power at its specified reference point -
(G_t): transmit antenna gain toward the receiver - (L_t):
transmitter-side losses not already included in (P_t) or realized
antenna gain - (FSPL): free-space path loss - (G_r): receive antenna
gain toward the transmitter - (L_r): receiver-side losses before the
chosen receiver reference point - (L\_{other}): additional applicable
losses not already included elsewhere

The (L\_{other}) term may include atmospheric attenuation, polarization
mismatch, pointing loss, or implementation-related degradation if those
effects are appropriately represented as power losses. Some effects,
such as Doppler and modem performance, are better analysed separately
rather than treated as simple power losses.

A more complete digital link analysis calculates (C/N_0), available
(E_b/N_0), the required (E_b/N_0), and margin, using consistent
reference points and definitions.

## 17. Recommended Calculation Workflow

1.  Define the link direction: downlink, uplink, or inter-satellite.
2.  Define the operating frequency, modulation, coding, bit rate, and
    target error performance.
3.  Define the orbit, ground-station location, minimum elevation angle,
    and slant-range cases.
4.  Record transmitter output power and the reference point for that
    power.
5.  Record transmitter and receiver antenna gains at the relevant angles
    and polarizations.
6.  Identify cable, connector, filter, switch, polarization, pointing,
    and propagation losses.
7.  Calculate EIRP.
8.  Calculate FSPL for the selected slant range.
9.  Calculate received power.
10. Estimate system noise temperature or noise figure and effective
    noise bandwidth.
11. Calculate (C/N), (C/N_0), and available (E_b/N_0), as appropriate.
12. Determine the required (E_b/N_0) or receiver sensitivity for the
    chosen modem and target error rate.
13. Calculate link margin.
14. Repeat for worst-case conditions and throughout the satellite pass.
15. Check useful data volume, power consumption, thermal constraints,
    regulatory limits, and operational availability.
16. Document assumptions, sources, uncertainty, and items that need
    verification by testing.

## 18. Example: Illustrative CubeSat Downlink

Assume the following values purely for demonstrating the arithmetic:

  Parameter                    Illustrative value
  -------------------------- --------------------
  Carrier frequency                       437 MHz
  Slant range                            1,000 km
  Transmitter output power            1 W = 0 dBW
  Transmit antenna gain                     0 dBi
  Transmitter-side losses                    1 dB
  Receive antenna gain                     10 dBi
  Receiver-side losses                       1 dB

### Step 1: Calculate EIRP

$$
EIRP = 0 + 0 - 1 = -1\ \text{dBW}
$$

### Step 2: Calculate free-space path loss

$$
FSPL = 32.44 + 20\log_{10}(437) + 20\log_{10}(1000)
$$

$$
FSPL \approx 32.44 + 52.81 + 60 = 145.25\ \text{dB}
$$

Small differences may occur due to rounding.

### Step 3: Calculate received power

$$
P_r = -1 - 145.25 + 10 - 1
$$

$$
P_r \approx -137.25\ \text{dBW}
$$

Converting to dBm:

$$
P_r \approx -107.25\ \text{dBm}
$$

This is a received-power estimate, not proof that the selected receiver
can decode the signal. Receiver noise, bandwidth, modulation, coding,
interference, and implementation losses must still be assessed.

### Step 4: Continue the analysis

To complete the example, you would still need to define: - Receiver
system noise temperature or noise figure - Effective noise bandwidth -
Bit rate and the bit-rate convention - Modulation and coding scheme -
Required BER or packet error rate - Required (E_b/N_0) under those
conditions - Additional losses and desired engineering margin

Without these, a defensible final link margin cannot be calculated.

## 19. Common Mistakes to Avoid

1.  Using satellite altitude instead of slant range in FSPL.
2.  Mixing MHz with a formula that expects GHz, or metres with a formula
    that expects kilometres.
3.  Mixing dBW and dBm without converting.
4.  Treating dBi as dB of power or adding antenna gain twice.
5.  Counting cable loss twice or forgetting losses before the receiver.
6.  Assuming receiver sensitivity is universal without specifying
    bandwidth and error-rate conditions.
7.  Using channel bandwidth automatically as the noise bandwidth.
8.  Confusing (C/N), (C/N_0), and (E_b/N_0).
9.  Using peak antenna gain when the antenna is mispointed or the
    satellite is in another direction.
10. Ignoring the worst point of the satellite pass.
11. Treating Doppler shift as a simple power loss.
12. Assuming a positive link margin guarantees successful communication.
13. Ignoring coding overhead, packet framing, and protocol inefficiency
    when estimating useful data volume.
14. Including the same implementation or propagation effect in multiple
    loss terms.
15. Using assumed component specifications as though they were verified
    hardware values.

## 20. Suggested Learning Order

For a learner developing a CubeSat communications subsystem, study these
topics in order:

1.  **RF fundamentals:** frequency, wavelength, power, dB, dBm, dBW, and
    dBi.
2.  **Propagation:** line of sight, slant range, FSPL, and elevation
    angle.
3.  **Transmitter and antennas:** output power, feeder loss, gain, EIRP,
    antenna pattern, and polarization.
4.  **Receiver and noise:** sensitivity, thermal noise, noise figure,
    and system noise temperature.
5.  **Digital link performance:** bandwidth, bit rate, (C/N), (C/N_0),
    (E_b/N_0), modulation, coding, and BER.
6.  **Link margin:** required performance, nominal cases, worst-case
    cases, and uncertainty.
7.  **Satellite-specific effects:** Doppler, pass geometry, pointing,
    spacecraft attitude, and contact time.
8.  **End-to-end design:** uplink and downlink budgets, data volume per
    pass, availability, power, thermal, and regulatory constraints.
9.  **Automation and validation:** build a spreadsheet or Python
    calculator, check units, test known cases, and validate assumptions
    against component data sheets and mission requirements.

## 21. Reference Checklist for a Link Budget Spreadsheet

A practical spreadsheet should include, at minimum:

### Link definition

-   Link direction and endpoints
-   Carrier frequency
-   Slant range or orbital geometry case
-   Required bit rate and useful data rate
-   Modulation, coding, and target error rate

### Transmitter

-   Transmitter output power and reference point
-   Transmitter-side cable and component losses
-   Transmit antenna gain in the relevant direction
-   EIRP

### Propagation

-   Free-space path loss
-   Atmospheric attenuation where applicable
-   Polarization mismatch loss
-   Pointing loss
-   Other justified propagation or implementation losses

### Receiver

-   Receive antenna gain
-   Receiver-side feeder and component losses
-   Received power
-   Noise figure or system noise temperature
-   Effective noise bandwidth
-   Noise power or noise spectral density

### Digital performance

-   (C/N)
-   (C/N_0)
-   Bit rate and its definition
-   Available (E_b/N_0)
-   Required (E_b/N_0) or verified receiver threshold
-   Link margin
-   BER/PER target and expected useful throughput

### Mission analysis

-   Minimum, nominal, and maximum slant range
-   Minimum elevation angle
-   Doppler shift and receiver acquisition range
-   Contact duration and usable pass time
-   Data volume per pass
-   Power and thermal constraints
-   Regulatory constraints
-   Assumptions, uncertainty, sources, and verification status

## 22. Final Engineering Principle

A link budget should be treated as a traceable engineering argument:
every number needs a unit, a reference point, a source or assumption,
and a clear explanation of whether it represents a gain, loss,
requirement, or calculated result.

For a CubeSat mission, the objective is not merely to obtain a positive
received-power value. The objective is to demonstrate that the selected
radio system can meet the mission's data-rate, error-performance,
availability, power, and operational requirements over the expected
range of satellite and ground-station conditions.
