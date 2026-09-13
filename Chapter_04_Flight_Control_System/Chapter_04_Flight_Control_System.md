**Volume 18. Cargo UAV Architecture**


# Chapter 04. Flight Control System

##  

## 04.01. Flight Control Computer

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

The Flight Control Computer (FCC) is the real-time computational core of a UAV flight control system, transforming aircraft state information and mission-level commands into deterministic actuator commands. In a cargo UAV, the FCC must maintain controlled flight despite disturbances, sensor errors, payload variation, communication loss, and selected equipment failures. It therefore combines high-rate computation, deterministic execution, fault monitoring, and safety-oriented interfaces within a tightly controlled avionics environment.

The FCC receives information from inertial measurement units, air-data sensors, GNSS receivers, attitude and heading reference systems, propulsion controllers, actuator feedback sensors, and other aircraft subsystems. These measurements represent different physical quantities, update rates, latencies, and uncertainty levels. The computer must acquire and validate them predictably so that the control algorithms operate on a coherent representation of aircraft motion rather than on unrelated asynchronous measurements.

A fundamental FCC function is estimation of the aircraft state required for stabilization and guidance. Raw accelerometer, gyroscope, magnetic, pressure, position, velocity, and other measurements may contain bias, noise, drift, or transient errors. The flight control system combines validated measurements to estimate attitude, angular rates, velocity, position, altitude, and related dynamic states. Reliable estimation is especially important when a cargo UAV transitions between operating modes or encounters rapidly changing aerodynamic conditions.

Flight control computation is normally organized as interacting control loops operating at different rates. Fast inner loops stabilize angular rates and attitude, while outer loops regulate quantities such as velocity, altitude, flight path, heading, and position. Guidance functions provide references to these controllers according to the active flight mode. The FCC continuously calculates control errors and generates commands for aerodynamic surfaces, propulsion units, rotor systems, or other effectors appropriate to the UAV configuration.

Deterministic timing is as important as computational performance. A flight controller that produces mathematically correct results too late can still destabilize the aircraft. FCC software is therefore executed according to carefully defined periods, priorities, deadlines, and worst-case execution assumptions. High-rate stabilization tasks may execute much faster than navigation, health monitoring, communication, or mission-management functions, while scheduling prevents lower-criticality workloads from interfering with time-critical control calculations.

The FCC must also manage the interfaces between flight-control algorithms and physical actuators. Commands may be transmitted to servo controllers, motor controllers, propulsion control units, or distributed remote I/O modules through dedicated electrical interfaces or avionics networks. Command limiting, rate limiting, saturation handling, actuator-position feedback, and plausibility monitoring help prevent an erroneous computation or failed actuator from immediately becoming an uncontrolled aircraft response.

Cargo UAV operation makes mass properties particularly important. Loading and unloading cargo changes gross weight, center of gravity, inertia, propulsion demand, and sometimes aerodynamic response. The FCC may therefore receive validated mass and center-of-gravity information from higher-level aircraft or cargo-management functions and apply appropriate control parameters or operating limits. A controller designed around a single nominal loading condition may otherwise provide inadequate stability margins across the aircraft\'s complete payload envelope.

Flight-mode management determines which control laws, references, protections, and actuator strategies are active during each phase of operation. Depending on aircraft architecture, modes can include ground operation, takeoff, climb, cruise, approach, landing, hover, transition, emergency operation, or degraded control. Mode transitions require explicit entry conditions and consistency checks because an unintended transition can be more dangerous than remaining temporarily in a degraded but stable mode.

Fault detection is consequently integrated closely with FCC operation. Sensor values can be checked for range, rate, consistency, freshness, and disagreement with redundant sources. Actuator responses can be compared with commanded behavior, while processor, memory, power, communication, and timing functions can be monitored independently. Detected faults are classified according to their effect so that the system can reject invalid information, isolate failed channels, reconfigure control, or initiate a predefined failsafe response.

Redundancy becomes increasingly important as cargo UAV size and consequence of failure increase. Multiple flight-control channels may independently acquire sensor data and calculate aircraft commands, with comparison or voting mechanisms used to identify disagreement. Redundancy is not simply duplication: power supplies, clocks, communication paths, sensors, I/O circuitry, and software dependencies must be considered because duplicated computers connected to the same vulnerable resource can still fail simultaneously from a common cause.

The FCC architecture must therefore address common-cause and common-mode failures as well as individual component failures. Physical separation, independent power domains, diverse sensing, partitioned communication paths, watchdog mechanisms, and carefully controlled reset behavior can prevent one fault from propagating through the entire flight-control system. For highly critical functions, system designers evaluate whether redundancy provides genuine independence rather than merely increasing the number of identical processing units.

Communication architecture strongly influences FCC integration. The computer may exchange deterministic control information with remote avionics while receiving lower-rate configuration, diagnostic, and mission information from other systems. Network traffic must be separated according to timing and criticality so that large data transfers cannot delay essential control messages. Interface design therefore considers message rate, latency, jitter, timeout behavior, integrity checking, synchronization, and behavior after communication interruption.

Time synchronization is particularly significant in distributed avionics. Sensor measurements obtained at different moments can create apparent physical inconsistencies even when every sensor is individually accurate. Accurate timestamps and synchronized clocks allow the FCC to associate measurements with the correct aircraft state and compensate for known transport delays. This becomes increasingly important when high-dynamic motion, distributed IMUs, remote actuators, advanced perception sensors, or networked flight-control components are introduced.

FCC hardware must operate within demanding environmental constraints while maintaining predictable behavior. Processor capability, memory architecture, I/O resources, power consumption, thermal design, electromagnetic compatibility, vibration resistance, and environmental qualification all influence the final implementation. Computational margin is deliberately maintained so that worst-case workloads, diagnostic activity, transient communication demand, and future software growth do not consume the resources required for deterministic flight control.

Software architecture should preserve separation between safety-critical control functions and less critical services. Hardware abstraction, device drivers, sensor processing, state estimation, control laws, mode management, fault management, communication services, and built-in test functions can be organized into controlled layers or partitions. Such separation improves verification and limits fault propagation while making it easier to trace system requirements through software functions, interfaces, tests, and certification evidence.

Startup and shutdown behavior are also safety-relevant. After power application, the FCC must establish processor health, memory integrity, sensor availability, communication status, configuration validity, and actuator readiness before permitting active flight control. Built-in tests can identify failures before takeoff, while continuous monitoring detects faults during flight. Reset strategies must be carefully designed because an uncontrolled processor restart during a critical flight phase may itself constitute a hazardous event.

The relationship between the FCC and higher-level autonomy requires a clear authority boundary. Mission planning or autonomous decision systems may request destinations, trajectories, velocities, or flight modes, but the FCC remains responsible for executing commands within validated aircraft constraints. This separation prevents an AI or mission-level function from directly commanding unsafe actuator behavior. Safety monitors can reject references that violate flight envelopes, rate limits, geofencing constraints, or currently available control capability.

For autonomous cargo aircraft, this layered relationship enables sophisticated autonomy without making basic aircraft stability dependent on high-level intelligence. Perception and planning systems can optimize routes, detect obstacles, select landing areas, or respond to changing missions, while deterministic FCC functions continue controlling the vehicle. If autonomy becomes unavailable, the flight-control architecture should retain sufficient independent capability to maintain safe aircraft behavior according to the defined degraded-operation strategy.

Verification of an FCC extends from individual algorithms to integrated aircraft behavior. Control laws can first be evaluated through mathematical simulation, followed by software-in-the-loop and hardware-in-the-loop testing. Processor timing, communication faults, sensor failures, actuator failures, power disturbances, and abnormal mode transitions can then be injected systematically. Ground testing and flight testing provide progressively stronger evidence that the implemented controller behaves as intended across normal, boundary, and failure conditions.

For a scalable cargo UAV family, the FCC should support growth from smaller aircraft toward heavier and more complex platforms without assuming that one hardware configuration can simply be enlarged indefinitely. Increasing payload, propulsion complexity, actuator count, redundancy requirements, and flight consequence can drive changes in processing architecture and system assurance. A well-defined FCC platform therefore separates reusable control concepts from aircraft-specific configuration, interfaces, performance limits, and safety mechanisms.

Ultimately, the Flight Control Computer forms the bridge between aircraft dynamics and digital intelligence. Its purpose is not merely to execute autopilot software, but to provide a deterministic, monitored, fault-tolerant control authority capable of maintaining safe flight under real operational conditions. Within the Cargo UAV Architecture, it becomes the central execution element connecting sensing, estimation, control laws, actuators, propulsion, avionics communication, failsafe logic, and higher-level autonomous mission functions.

비행제어컴퓨터(Flight Control Computer, FCC)는 무인항공기(UAV) 비행제어시스템(Flight Control System)의 실시간 연산 핵심으로서, 항공기 상태 정보와 임무 수준 명령을 결정론적 액추에이터 명령(Deterministic Actuator Command)으로 변환한다. 화물 무인항공기(Cargo UAV)에서 FCC는 외란, 센서 오류, 탑재화물 변화, 통신 두절 및 특정 장비 고장이 발생하더라도 제어 가능한 비행 상태를 유지해야 한다. 따라서 엄격하게 관리되는 항공전자(Avionics) 환경에서 고속 연산, 결정론적 실행, 고장 감시 및 안전 중심 인터페이스를 통합한다.

FCC는 관성측정장치(Inertial Measurement Unit, IMU), 대기자료센서(Air-Data Sensor), 위성항법시스템(Global Navigation Satellite System, GNSS) 수신기, 자세방위기준시스템(Attitude and Heading Reference System, AHRS), 추진제어기(Propulsion Controller), 액추에이터 피드백 센서 및 기타 항공기 서브시스템으로부터 정보를 수신한다. 이러한 측정값은 서로 다른 물리량, 갱신 주기, 지연시간(Latency) 및 불확실성을 가진다. FCC는 제어 알고리즘이 서로 무관한 비동기 측정값이 아니라 일관된 항공기 운동 상태를 기반으로 동작하도록 데이터를 예측 가능한 방식으로 획득하고 검증해야 한다.

FCC의 기본 기능 중 하나는 항공기 안정화(Stabilization)와 유도(Guidance)에 필요한 상태를 추정하는 것이다. 가속도계, 자이로스코프, 자기장, 압력, 위치, 속도 등의 원시 측정값에는 바이어스(Bias), 노이즈(Noise), 드리프트(Drift) 또는 일시적인 오류가 포함될 수 있다. 비행제어시스템은 검증된 측정값을 결합하여 자세(Attitude), 각속도(Angular Rate), 속도(Velocity), 위치(Position), 고도(Altitude) 및 관련 동적 상태를 추정한다. 신뢰성 높은 상태 추정은 화물 UAV가 운용 모드 사이를 전환하거나 급격하게 변화하는 공력 조건에 직면할 때 특히 중요하다.

비행제어 연산(Flight Control Computation)은 일반적으로 서로 다른 주기로 동작하는 상호 연계된 제어 루프(Control Loop)로 구성된다. 빠른 내부 루프(Inner Loop)는 각속도와 자세를 안정화하고, 외부 루프(Outer Loop)는 속도, 고도, 비행경로, 방위 및 위치 등을 제어한다. 유도 기능(Guidance Function)은 현재 활성화된 비행 모드에 따라 이러한 제어기에 기준값을 제공한다. FCC는 제어 오차를 지속적으로 계산하고 UAV 구성에 적합한 공력 조종면, 추진장치, 로터 시스템 또는 기타 제어효과기(Effector)에 대한 명령을 생성한다.

결정론적 타이밍(Deterministic Timing)은 연산 성능만큼 중요하다. 수학적으로 정확한 결과를 계산하더라도 너무 늦게 출력하는 비행제어기는 항공기를 불안정하게 만들 수 있다. 따라서 FCC 소프트웨어는 명확하게 정의된 실행 주기, 우선순위, 마감시간(Deadline) 및 최악실행시간(Worst-Case Execution Time) 가정에 따라 동작한다. 고속 안정화 작업은 항법, 상태 감시, 통신 또는 임무관리 기능보다 훨씬 빠르게 실행될 수 있으며, 스케줄링(Scheduling)을 통해 낮은 중요도의 작업이 시간 임계적인 제어 연산을 방해하지 않도록 한다.

FCC는 비행제어 알고리즘과 물리적 액추에이터(Actuator) 사이의 인터페이스도 관리해야 한다. 명령은 전용 전기 인터페이스 또는 항공전자 네트워크를 통해 서보제어기(Servo Controller), 모터제어기(Motor Controller), 추진제어장치(Propulsion Control Unit) 또는 분산형 원격 입출력 모듈(Remote I/O Module)로 전달될 수 있다. 명령 제한(Command Limiting), 변화율 제한(Rate Limiting), 포화 처리(Saturation Handling), 액추에이터 위치 피드백 및 타당성 감시(Plausibility Monitoring)는 잘못된 연산이나 액추에이터 고장이 즉각적인 항공기 제어 상실로 이어지는 것을 방지한다.

화물 UAV 운용에서는 질량 특성(Mass Properties)이 특히 중요하다. 화물의 적재와 하역은 총중량(Gross Weight), 무게중심(Center of Gravity, CG), 관성(Inertia), 추진 요구량 및 경우에 따라 공력 응답까지 변화시킨다. 따라서 FCC는 상위 수준의 항공기 또는 화물관리 기능으로부터 검증된 질량 및 무게중심 정보를 받아 적절한 제어 파라미터나 운용 제한을 적용할 수 있다. 단일 기준 적재조건만을 기준으로 설계된 제어기는 항공기의 전체 탑재중량 영역(Payload Envelope)에서 충분한 안정성 여유(Stability Margin)를 제공하지 못할 수 있다.

비행모드관리(Flight-Mode Management)는 각 운용 단계에서 어떤 제어법칙(Control Law), 기준값, 보호기능 및 액추에이터 전략을 활성화할 것인지를 결정한다. 항공기 아키텍처에 따라 지상운용, 이륙, 상승, 순항, 접근, 착륙, 호버링(Hover), 전환비행(Transition), 비상운용 또는 성능저하 제어(Degraded Control) 등의 모드를 포함할 수 있다. 의도하지 않은 모드 전환은 일시적으로 성능이 저하되더라도 안정적인 모드를 유지하는 것보다 위험할 수 있으므로, 모드 전환에는 명확한 진입 조건과 일관성 검사가 필요하다.

따라서 고장검출(Fault Detection)은 FCC 동작과 긴밀하게 통합된다. 센서 값은 범위, 변화율, 일관성, 최신성(Freshness) 및 중복 센서 간 불일치 여부를 기준으로 검사할 수 있다. 액추에이터 응답은 명령된 동작과 비교할 수 있으며, 프로세서, 메모리, 전원, 통신 및 타이밍 기능도 독립적으로 감시할 수 있다. 검출된 고장은 영향도에 따라 분류되며, 시스템은 잘못된 정보를 배제하거나 고장 채널을 격리하고 제어를 재구성하거나 사전에 정의된 비상안전대응(Failsafe Response)을 시작할 수 있다.

화물 UAV의 크기와 고장 결과의 심각성이 증가할수록 이중화(Redundancy)의 중요성도 커진다. 여러 비행제어 채널이 독립적으로 센서 데이터를 획득하고 항공기 제어 명령을 계산하며, 비교 또는 투표 메커니즘(Voting Mechanism)을 사용하여 채널 간 불일치를 식별할 수 있다. 그러나 이중화는 단순한 복제가 아니다. 전원공급장치, 클록(Clock), 통신 경로, 센서, 입출력 회로 및 소프트웨어 의존성까지 고려해야 한다. 동일한 취약 자원에 연결된 여러 컴퓨터는 동시에 고장날 수 있기 때문이다.

따라서 FCC 아키텍처는 개별 부품 고장뿐 아니라 공통원인고장(Common-Cause Failure)과 공통모드고장(Common-Mode Failure)도 고려해야 한다. 물리적 분리, 독립적인 전원 도메인(Power Domain), 다양한 센싱 방식, 분리된 통신 경로, 워치독 메커니즘(Watchdog Mechanism) 및 신중하게 설계된 리셋 동작은 하나의 고장이 전체 비행제어시스템으로 전파되는 것을 방지할 수 있다. 고도의 안전성이 요구되는 기능에서는 단순히 동일한 처리장치의 수를 증가시키는 것이 아니라 이중화가 실제 독립성을 제공하는지 평가해야 한다.

통신 아키텍처(Communication Architecture)는 FCC 통합 방식에 큰 영향을 미친다. FCC는 원격 항공전자 장치와 결정론적인 제어 정보를 교환하는 동시에 다른 시스템으로부터 상대적으로 낮은 주기의 구성, 진단 및 임무 정보를 수신할 수 있다. 대용량 데이터 전송이 필수 제어 메시지를 지연시키지 않도록 네트워크 트래픽은 타이밍과 중요도에 따라 분리되어야 한다. 따라서 인터페이스 설계에서는 메시지 주기, 지연시간, 지터(Jitter), 타임아웃(Timeout), 무결성 검사, 동기화 및 통신 중단 이후의 동작을 고려한다.

시간동기화(Time Synchronization)는 분산형 항공전자(Distributed Avionics)에서 특히 중요하다. 서로 다른 시점에서 획득된 센서 측정값은 각각의 센서가 정확하더라도 물리적으로 서로 모순되는 것처럼 보일 수 있다. 정확한 타임스탬프(Timestamp)와 동기화된 클록을 사용하면 FCC가 측정값을 올바른 항공기 상태와 연결하고 알려진 전송 지연을 보상할 수 있다. 이러한 기능은 고동적 운동, 분산형 IMU, 원격 액추에이터, 첨단 인지센서 또는 네트워크 기반 비행제어 구성요소가 적용될수록 더욱 중요해진다.

FCC 하드웨어는 까다로운 환경 조건에서도 예측 가능한 동작을 유지해야 한다. 프로세서 성능, 메모리 아키텍처, 입출력 자원, 전력소비, 열설계(Thermal Design), 전자파적합성(Electromagnetic Compatibility, EMC), 진동 내성 및 환경 적합성 검증(Environmental Qualification)은 최종 구현에 모두 영향을 준다. 최악 조건의 작업부하, 진단 활동, 일시적인 통신 부하 및 향후 소프트웨어 확장이 결정론적 비행제어에 필요한 자원을 침범하지 않도록 충분한 연산 여유(Computational Margin)를 확보해야 한다.

소프트웨어 아키텍처(Software Architecture)는 안전 중요 제어기능(Safety-Critical Control Function)과 상대적으로 중요도가 낮은 서비스 사이의 분리를 유지해야 한다. 하드웨어 추상화(Hardware Abstraction), 장치 드라이버, 센서 처리, 상태 추정, 제어법칙, 모드관리, 고장관리, 통신 서비스 및 내장시험(Built-In Test, BIT) 기능을 제어된 계층 또는 파티션(Partition)으로 구성할 수 있다. 이러한 분리는 검증을 용이하게 하고 고장 전파를 제한하며, 시스템 요구사항을 소프트웨어 기능, 인터페이스, 시험 및 인증 근거까지 추적하기 쉽게 만든다.

시작 및 종료 동작(Startup and Shutdown Behavior) 역시 안전과 관련된다. 전원이 인가된 후 FCC는 능동 비행제어를 허용하기 전에 프로세서 상태, 메모리 무결성, 센서 가용성, 통신 상태, 구성정보 유효성 및 액추에이터 준비 상태를 확인해야 한다. 내장시험은 이륙 전에 고장을 식별할 수 있으며, 연속 감시는 비행 중 발생하는 고장을 검출한다. 특히 중요한 비행 단계에서 제어되지 않은 프로세서 재시작은 그 자체가 위험 사건이 될 수 있으므로 리셋 전략(Reset Strategy)을 신중하게 설계해야 한다.

FCC와 상위 수준 자율시스템(Autonomy System)의 관계에서는 명확한 제어권 경계(Authority Boundary)가 필요하다. 임무계획 또는 자율 의사결정 시스템은 목적지, 궤적, 속도 또는 비행모드를 요청할 수 있지만, FCC는 검증된 항공기 제약조건 안에서 이러한 명령을 실행할 책임을 가진다. 이러한 분리는 인공지능(AI)이나 임무 수준 기능이 위험한 액추에이터 동작을 직접 명령하는 것을 방지한다. 안전 감시기는 비행영역(Flight Envelope), 변화율 제한, 지오펜싱(Geofencing) 제약 또는 현재 이용 가능한 제어 능력을 위반하는 기준 명령을 거부할 수 있다.

자율 화물항공기(Autonomous Cargo Aircraft)에서는 이러한 계층적 관계를 통해 기본적인 항공기 안정성을 상위 수준 지능에 의존시키지 않으면서도 고도화된 자율기능을 구현할 수 있다. 인지 및 계획 시스템은 경로를 최적화하고 장애물을 감지하며 착륙지역을 선택하거나 변화하는 임무에 대응할 수 있지만, 결정론적인 FCC 기능은 계속해서 항공기를 제어한다. 자율기능을 사용할 수 없게 되더라도 비행제어 아키텍처는 정의된 성능저하 운용전략(Degraded-Operation Strategy)에 따라 안전한 항공기 동작을 유지할 수 있는 충분한 독립 기능을 보유해야 한다.

FCC 검증(Verification)은 개별 알고리즘에서 통합 항공기 동작까지 확장된다. 제어법칙은 먼저 수학적 시뮬레이션을 통해 평가하고, 이후 소프트웨어 인더 루프(Software-in-the-Loop, SIL)와 하드웨어 인더 루프(Hardware-in-the-Loop, HIL) 시험으로 발전시킬 수 있다. 프로세서 타이밍, 통신 고장, 센서 고장, 액추에이터 고장, 전원 이상 및 비정상적인 모드 전환 등을 체계적으로 주입하여 검증할 수 있다. 지상시험과 비행시험은 구현된 제어기가 정상, 경계 및 고장 조건 전반에서 의도한 대로 동작한다는 더욱 강력한 근거를 제공한다.

확장 가능한 화물 UAV 제품군(Scalable Cargo UAV Family)의 경우 FCC는 하나의 하드웨어 구성을 무한히 확장할 수 있다고 가정하지 않으면서 소형 항공기에서 더 무겁고 복잡한 플랫폼으로 발전할 수 있도록 설계되어야 한다. 탑재중량, 추진 복잡도, 액추에이터 수, 이중화 요구사항 및 고장 결과의 심각성이 증가하면 처리 아키텍처와 시스템 보증(System Assurance) 방식도 변화할 수 있다. 따라서 잘 정의된 FCC 플랫폼은 재사용 가능한 제어 개념과 항공기별 구성, 인터페이스, 성능 한계 및 안전 메커니즘을 명확하게 분리해야 한다.

궁극적으로 비행제어컴퓨터(Flight Control Computer)는 항공기 동역학(Aircraft Dynamics)과 디지털 지능(Digital Intelligence)을 연결하는 핵심 요소이다. FCC의 목적은 단순히 자동조종 소프트웨어(Autopilot Software)를 실행하는 것이 아니라 실제 운용 조건에서 안전한 비행을 유지할 수 있는 결정론적이고 감시 가능하며 내고장성(Fault-Tolerant)을 갖춘 제어 권한을 제공하는 것이다. 화물 UAV 아키텍처(Cargo UAV Architecture)에서 FCC는 센싱, 상태 추정, 제어법칙, 액추에이터, 추진시스템, 항공전자 통신, 비상안전 로직(Failsafe Logic) 및 상위 수준 자율 임무기능을 연결하는 중앙 실행 요소가 된다.

##  

## 04.02. IMU/AHRS Integration

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

An Inertial Measurement Unit (IMU) and an Attitude and Heading Reference System (AHRS) form the primary motion-sensing foundation of a UAV flight control system. The IMU measures physical motion directly, while the AHRS converts inertial and complementary sensor information into estimates of aircraft attitude, heading, and angular motion. Their integration provides the Flight Control Computer (FCC) with a continuously updated representation of vehicle orientation and dynamics required for stabilization, guidance, navigation, and autonomous flight.

A typical IMU contains three-axis gyroscopes and three-axis accelerometers arranged to measure angular velocity and specific force along orthogonal body axes. Higher-performance units may also incorporate temperature sensing, internal calibration, signal conditioning, and diagnostic functions. The gyroscopes provide rapid information about rotational motion, while accelerometers respond to translational acceleration and gravity-related effects. Together, these measurements allow the flight control system to observe short-term aircraft dynamics at high update rates.

Raw inertial measurements cannot directly provide reliable long-term attitude information. Gyroscope measurements contain bias and noise that accumulate during numerical integration, producing orientation drift over time. Accelerometers provide an independent reference related to gravity when dynamic acceleration is limited, but they are disturbed during maneuvering. Consequently, practical UAV systems combine multiple measurements rather than relying on a single inertial sensor to determine aircraft orientation continuously.

The AHRS performs this fusion by combining gyroscope and accelerometer measurements with additional references such as magnetometers, GNSS-derived information, or other navigation sensors. Sensor-fusion algorithms estimate roll, pitch, heading, angular rates, and associated error states while compensating for measurement uncertainty. The resulting attitude solution is more stable than direct integration of gyroscope data and more responsive than an orientation estimate derived only from slower external references.

Coordinate-frame management is fundamental to correct IMU and AHRS integration. Sensor measurements originate in the local sensor frame, while flight-control algorithms generally operate using defined aircraft body, navigation, or Earth-referenced frames. The installation orientation of each IMU must therefore be known accurately. Rotation matrices, quaternions, or equivalent transformations are used to convert measurements between coordinate systems while maintaining consistent axis directions and sign conventions throughout the avionics architecture.

Quaternions are widely suitable for representing UAV attitude because they avoid the singularities associated with some Euler-angle representations and support efficient rotational calculations. Roll, pitch, and yaw remain useful for human interpretation, displays, and selected control interfaces, but the internal attitude estimator may maintain orientation as a quaternion. Consistency between mathematical representations is essential because an incorrect transformation or axis convention can create control errors even when every sensor operates correctly.

Timing accuracy is equally important. Gyroscope and accelerometer samples must be associated with precise acquisition times because the aircraft may rotate significantly between measurements. Timestamp errors, communication latency, or irregular sampling intervals can introduce estimation errors that appear similar to sensor noise. The FCC should therefore process inertial data using known sampling periods, synchronized clocks, and predictable communication paths, particularly when IMUs and flight-control processors are physically distributed.

The IMU interface must also provide sufficient update rate and deterministic latency for the control architecture. High-rate inertial measurements normally support fast stabilization loops, whereas GNSS, magnetometer, air-data, and other complementary measurements may arrive more slowly. The estimator must accommodate these asynchronous rates without allowing delayed information to corrupt the current state. Buffering, timestamp-based alignment, interpolation, or propagation techniques can be used to associate measurements with the appropriate estimated aircraft state.

Calibration determines how accurately raw sensor outputs represent actual motion. Accelerometer scale factor, gyroscope scale factor, zero bias, axis misalignment, temperature dependence, and cross-axis sensitivity can all affect the estimated attitude. Factory calibration provides an initial characterization, but aircraft-level integration must also consider installation alignment and environmental effects. Calibration parameters should be controlled configuration data so that the FCC applies the correct compensation for the installed sensor hardware.

Temperature is a particularly important source of inertial-sensor error because bias and scale characteristics may change as avionics warm up or encounter different operating environments. An IMU may include internal temperature compensation, while the AHRS or FCC can apply additional correction based on calibrated models. Startup behavior must account for sensor stabilization because measurements obtained immediately after power application may have different characteristics from those produced after the system reaches thermal equilibrium.

Vibration can significantly degrade inertial sensing in UAVs. Propellers, rotors, motors, engines, gearboxes, structural modes, and aerodynamic excitation can introduce mechanical energy into the IMU frequency range. Mechanical mounting, structural placement, filtering, and sensor bandwidth must therefore be considered together. Excessive filtering can add phase delay, while insufficient filtering can allow vibration-induced noise to propagate into state estimation and flight-control commands.

Sensor filtering must preserve the aircraft dynamics required by the controller. Low-pass filters can suppress high-frequency noise, notch filters can attenuate known vibration frequencies, and estimator algorithms can statistically balance different measurements. However, filtering cannot simply be maximized because every filter introduces some combination of delay, attenuation, or phase distortion. IMU signal conditioning must therefore be designed as part of the complete control-loop architecture rather than as an isolated sensor function.

Redundant IMUs can improve availability and fault tolerance in safety-critical cargo UAVs. Two or more independently powered sensing channels may provide simultaneous measurements to redundant FCC channels. Their outputs can be compared for disagreement, excessive bias, frozen data, implausible rates, timing errors, or communication failures. Triple-channel arrangements can support voting or fault isolation when system safety requirements justify the additional hardware and integration complexity.

Redundancy is effective only when common-cause failures are considered. Multiple identical IMUs mounted on the same structure may all experience the same excessive vibration, thermal condition, power disturbance, or electromagnetic interference. Physical separation, independent power paths, diverse sensor technologies, separate communication channels, and appropriate installation design can reduce these dependencies. The architecture should distinguish genuine sensing diversity from simple duplication of the same vulnerability.

Fault detection within the IMU/AHRS chain must operate continuously. Measurements can be checked against physical limits, previous samples, redundant sensors, estimated aircraft dynamics, and external references. A sudden impossible angular rate may indicate a sensor fault, while gradual divergence may indicate increasing bias. The estimator should identify suspect information before it destabilizes the control solution and transition toward available valid measurements according to predefined fault-management logic.

GNSS integration provides an important external reference for inertial navigation. The IMU offers high-rate short-term motion information but accumulates error, whereas GNSS provides bounded position and velocity information at a lower rate and can become unavailable or degraded. Combining them allows the navigation solution to exploit complementary characteristics. During temporary GNSS loss, inertial propagation can maintain continuity, although uncertainty grows until reliable external measurements become available again.

Magnetometers can provide heading information but require careful integration because aircraft electrical systems, motors, high-current cables, ferromagnetic structures, and payload equipment may distort the local magnetic field. Magnetic measurements should therefore be calibrated and monitored rather than treated as an unquestionable heading reference. Larger cargo UAVs may require thoughtful sensor placement or alternative heading references when propulsion and electrical architecture create significant magnetic disturbances.

The relationship between the AHRS and FCC depends on system partitioning. Some architectures use a smart AHRS that performs internal filtering and delivers completed attitude estimates, while others send calibrated raw IMU measurements to the FCC for centralized state estimation. A hybrid architecture may provide both raw measurements and independently computed attitude solutions. The appropriate choice depends on latency, redundancy, computational architecture, verification strategy, fault containment, and required system assurance.

For cargo UAVs, changes in payload can indirectly affect inertial estimation through altered vibration, structural response, acceleration characteristics, and center-of-gravity location. Although the IMU measures motion rather than cargo properties directly, its installation relative to the aircraft reference frame and center of rotation influences observed accelerations. Accurate configuration information becomes increasingly important as payload mass increases and the aircraft operates across a wider range of loading conditions.

Initialization is a critical operational phase for the AHRS. Before active flight, the system must establish sensor health, initial orientation, bias estimates, timing status, and availability of external references. Stationary alignment can improve initial bias and attitude estimates when operational conditions permit. The FCC should not assume that valid attitude information exists immediately after power-up, and readiness logic should distinguish between sensor communication availability and a fully converged navigation solution.

Verification should include sensor-level, estimator-level, and aircraft-level testing. Recorded data and simulation can evaluate fusion algorithms, while hardware-in-the-loop testing can reproduce motion profiles and inject timing errors, sensor bias, noise, dropouts, and failures. Ground tests can evaluate vibration and electromagnetic effects, and flight testing confirms performance under actual dynamic conditions. Particular attention should be given to transitions between normal, degraded, and redundant sensing configurations.

Within the cargo UAV architecture, IMU and AHRS integration ultimately provides the trusted dynamic state upon which flight control depends. The quality of this function is determined not only by sensor specifications but also by calibration, mounting, coordinate transformations, synchronization, filtering, redundancy, fault management, and estimator design. A robust integration architecture enables the FCC to maintain stable and predictable control while supporting increasingly autonomous operation across 2.5-ton, 5-ton, and future 10-ton cargo UAV platforms.

관성측정장치(Inertial Measurement Unit, IMU)와 자세방위기준시스템(Attitude and Heading Reference System, AHRS)은 무인항공기(UAV) 비행제어시스템(Flight Control System)의 핵심적인 운동 감지 기반을 구성한다. IMU는 물리적인 운동을 직접 측정하고, AHRS는 관성센서와 보조센서 정보를 항공기의 자세, 방위 및 각운동 추정값으로 변환한다. 두 시스템의 통합을 통해 비행제어컴퓨터(Flight Control Computer, FCC)는 안정화, 유도, 항법 및 자율비행에 필요한 기체 방향과 동역학 상태를 지속적으로 갱신하여 파악할 수 있다.

일반적인 IMU는 서로 직교하는 기체 축을 따라 각속도와 비력(Specific Force)을 측정하도록 구성된 3축 자이로스코프(Three-Axis Gyroscope)와 3축 가속도계(Three-Axis Accelerometer)를 포함한다. 고성능 장치는 온도 감지, 내부 보정, 신호처리 및 진단 기능을 추가로 포함할 수 있다. 자이로스코프는 회전운동에 대한 빠른 정보를 제공하고, 가속도계는 병진가속도와 중력 관련 영향에 반응한다. 이러한 측정값을 결합하면 비행제어시스템이 높은 갱신 주기로 항공기의 단기 동역학을 관측할 수 있다.

원시 관성 측정값(Raw Inertial Measurement)만으로는 장시간에 걸쳐 신뢰할 수 있는 자세 정보를 직접 제공하기 어렵다. 자이로스코프 측정값에는 바이어스(Bias)와 노이즈(Noise)가 포함되어 있으며, 이를 수치적으로 적분하면 시간이 지남에 따라 오차가 누적되어 자세 드리프트(Orientation Drift)가 발생한다. 가속도계는 동적 가속이 제한된 조건에서 중력과 관련된 독립적인 기준을 제공하지만 기동 중에는 영향을 받는다. 따라서 실제 UAV 시스템은 단일 관성센서에 의존하지 않고 여러 측정값을 결합하여 항공기 자세를 지속적으로 결정한다.

AHRS는 자이로스코프와 가속도계 측정값을 자력계(Magnetometer), 위성항법시스템(GNSS) 기반 정보 또는 기타 항법센서와 같은 추가 기준정보와 결합하여 센서융합(Sensor Fusion)을 수행한다. 센서융합 알고리즘은 측정 불확실성을 보상하면서 롤(Roll), 피치(Pitch), 방위(Heading), 각속도 및 관련 오차 상태를 추정한다. 이렇게 생성된 자세 해(Attitude Solution)는 자이로스코프 데이터만을 직접 적분한 결과보다 안정적이며, 느린 외부 기준정보만으로 생성한 자세 추정값보다 빠른 응답성을 제공한다.

좌표계 관리(Coordinate-Frame Management)는 IMU와 AHRS를 올바르게 통합하기 위한 기본 요소이다. 센서 측정값은 센서 자체의 로컬 좌표계(Local Sensor Frame)에서 생성되지만, 비행제어 알고리즘은 일반적으로 정의된 항공기 기체좌표계(Body Frame), 항법좌표계(Navigation Frame) 또는 지구기준좌표계(Earth-Referenced Frame)를 사용한다. 따라서 각 IMU의 장착 방향을 정확하게 알아야 한다. 회전행렬(Rotation Matrix), 쿼터니언(Quaternion) 또는 이에 상응하는 변환을 사용하여 전체 항공전자 아키텍처에서 축 방향과 부호 규칙을 일관되게 유지하면서 좌표계 사이의 측정값을 변환한다.

쿼터니언(Quaternion)은 일부 오일러각(Euler Angle) 표현에서 발생하는 특이점(Singularity)을 피하고 효율적인 회전 계산을 지원하기 때문에 UAV 자세 표현에 널리 적합하다. 롤, 피치, 요(Yaw)는 사람의 해석, 디스플레이 및 특정 제어 인터페이스에서 여전히 유용하지만, 내부 자세 추정기는 방향을 쿼터니언으로 유지할 수 있다. 모든 센서가 정상적으로 동작하더라도 잘못된 좌표변환이나 축 규칙은 제어오류를 발생시킬 수 있으므로 수학적 표현 간의 일관성이 매우 중요하다.

타이밍 정확도(Timing Accuracy)도 동일하게 중요하다. 항공기는 측정 사이의 짧은 시간에도 상당한 회전운동을 할 수 있으므로 자이로스코프와 가속도계 샘플은 정확한 획득 시각과 연결되어야 한다. 타임스탬프(Timestamp) 오류, 통신 지연 또는 불규칙한 샘플링 간격은 센서 노이즈와 유사한 상태추정 오류를 발생시킬 수 있다. 따라서 FCC는 특히 IMU와 비행제어 프로세서가 물리적으로 분산된 경우 정확한 샘플링 주기, 동기화된 클록 및 예측 가능한 통신 경로를 사용하여 관성 데이터를 처리해야 한다.

IMU 인터페이스는 제어 아키텍처에 충분한 갱신율(Update Rate)과 결정론적 지연시간(Deterministic Latency)을 제공해야 한다. 고속 관성 측정값은 일반적으로 빠른 안정화 제어루프를 지원하는 반면 GNSS, 자력계, 대기자료 및 기타 보조 측정값은 상대적으로 느리게 수신될 수 있다. 추정기는 이러한 비동기적인 데이터 주기를 처리하면서 지연된 정보가 현재 상태를 왜곡하지 않도록 해야 한다. 버퍼링(Buffering), 타임스탬프 기반 정렬, 보간(Interpolation) 또는 상태 전파(State Propagation) 기법을 사용하여 측정값을 적절한 항공기 추정 상태와 연결할 수 있다.

보정(Calibration)은 원시 센서 출력이 실제 운동을 얼마나 정확하게 나타내는지를 결정한다. 가속도계 스케일 팩터(Scale Factor), 자이로스코프 스케일 팩터, 영점 바이어스(Zero Bias), 축 정렬오차(Axis Misalignment), 온도 의존성 및 교차축 감도(Cross-Axis Sensitivity)는 모두 추정 자세에 영향을 줄 수 있다. 공장 보정은 초기 특성을 제공하지만 항공기 수준 통합에서는 장착 정렬과 환경 영향도 고려해야 한다. FCC가 설치된 센서 하드웨어에 적합한 보정을 적용할 수 있도록 보정 파라미터는 관리되는 구성 데이터(Configuration Data)로 취급해야 한다.

온도는 항공전자 장비가 가열되거나 서로 다른 운용환경에 노출될 때 바이어스와 스케일 특성을 변화시킬 수 있기 때문에 관성센서 오류의 중요한 원인이다. IMU 자체가 내부 온도보상(Temperature Compensation)을 포함할 수 있으며, AHRS 또는 FCC가 보정 모델을 기반으로 추가적인 보정을 적용할 수도 있다. 전원 인가 직후의 측정 특성이 시스템이 열적 평형(Thermal Equilibrium)에 도달한 이후와 다를 수 있으므로 초기 기동 과정에서는 센서 안정화 상태를 고려해야 한다.

진동(Vibration)은 UAV의 관성센서 성능을 크게 저하시킬 수 있다. 프로펠러, 로터, 모터, 엔진, 기어박스, 구조물 고유모드 및 공력 가진(Aerodynamic Excitation)은 IMU의 측정 주파수 영역으로 기계적 에너지를 전달할 수 있다. 따라서 기계적 장착, 구조적 배치, 필터링 및 센서 대역폭을 함께 고려해야 한다. 지나친 필터링은 위상지연(Phase Delay)을 증가시키고, 필터링이 부족하면 진동으로 발생한 노이즈가 상태추정과 비행제어 명령으로 전달될 수 있다.

센서 필터링(Sensor Filtering)은 제어기가 필요로 하는 항공기 동역학 정보를 보존해야 한다. 저역통과필터(Low-Pass Filter)는 고주파 노이즈를 억제하고, 노치필터(Notch Filter)는 알려진 특정 진동 주파수를 감쇠시키며, 추정 알고리즘은 서로 다른 측정값의 신뢰도를 통계적으로 조정할 수 있다. 그러나 모든 필터는 일정 수준의 지연, 감쇠 또는 위상왜곡을 발생시키므로 단순히 필터링 강도를 최대화할 수 없다. 따라서 IMU 신호처리는 독립적인 센서 기능이 아니라 전체 제어루프 아키텍처의 일부로 설계해야 한다.

중복 IMU(Redundant IMU)는 안전 중요 화물 UAV에서 가용성(Availability)과 내고장성(Fault Tolerance)을 향상시킬 수 있다. 독립적으로 전원을 공급받는 두 개 이상의 센싱 채널이 중복 FCC 채널에 동시에 측정값을 제공할 수 있다. 각 출력은 상호 비교를 통해 불일치, 과도한 바이어스, 데이터 고착(Frozen Data), 비정상적인 각속도, 타이밍 오류 또는 통신 장애를 검출할 수 있다. 시스템 안전 요구사항이 추가 하드웨어와 통합 복잡성을 정당화하는 경우 3중 채널 구성은 투표(Voting) 또는 고장격리(Fault Isolation)를 지원할 수 있다.

이중화(Redundancy)는 공통원인고장(Common-Cause Failure)을 고려할 때에만 효과적이다. 동일한 구조물에 장착된 여러 개의 동일한 IMU는 과도한 진동, 열환경, 전원 이상 또는 전자기 간섭(Electromagnetic Interference)을 동시에 경험할 수 있다. 물리적 분리, 독립 전원 경로, 서로 다른 센서 기술, 별도의 통신 채널 및 적절한 장착 설계를 통해 이러한 의존성을 줄일 수 있다. 시스템 아키텍처에서는 동일한 취약성을 단순히 복제하는 것과 실질적인 센싱 다양성(Sensing Diversity)을 명확히 구분해야 한다.

IMU/AHRS 체인의 고장검출(Fault Detection)은 지속적으로 수행되어야 한다. 측정값은 물리적 한계, 이전 샘플, 중복 센서, 추정된 항공기 동역학 및 외부 기준정보와 비교하여 검사할 수 있다. 갑작스럽고 물리적으로 불가능한 각속도는 센서 고장을 나타낼 수 있으며, 점진적인 편차 증가는 바이어스 증가를 의미할 수 있다. 추정기는 의심스러운 정보가 제어 해를 불안정하게 만들기 전에 이를 식별하고 사전에 정의된 고장관리 로직(Fault-Management Logic)에 따라 사용 가능한 정상 측정값으로 전환해야 한다.

GNSS 통합은 관성항법(Inertial Navigation)에 중요한 외부 기준을 제공한다. IMU는 높은 주기의 단기 운동정보를 제공하지만 시간이 지나면서 오차가 누적되는 반면, GNSS는 낮은 갱신 주기에서도 제한된 오차 범위의 위치 및 속도 정보를 제공하지만 신호가 손실되거나 성능이 저하될 수 있다. 두 시스템을 결합하면 서로 보완적인 특성을 활용할 수 있다. 일시적으로 GNSS가 손실되면 관성 상태 전파를 통해 항법 연속성을 유지할 수 있지만, 신뢰할 수 있는 외부 측정값이 다시 확보될 때까지 불확실성은 계속 증가한다.

자력계(Magnetometer)는 방위 정보를 제공할 수 있지만 항공기의 전기시스템, 모터, 대전류 케이블, 강자성 구조물 및 탑재장비가 국부 자기장을 왜곡할 수 있으므로 신중하게 통합해야 한다. 따라서 자기장 측정값은 절대적으로 신뢰할 수 있는 방위 기준으로 간주하기보다는 보정하고 지속적으로 감시해야 한다. 대형 화물 UAV에서는 추진시스템과 전기 아키텍처가 상당한 자기장 교란을 발생시키는 경우 센서의 장착 위치를 신중하게 결정하거나 대체 방위 기준을 사용할 필요가 있다.

AHRS와 FCC의 관계는 시스템 분할(System Partitioning) 방식에 따라 달라진다. 일부 아키텍처에서는 내부 필터링을 수행하고 완성된 자세 추정값을 출력하는 지능형 AHRS(Smart AHRS)를 사용하며, 다른 아키텍처에서는 보정된 원시 IMU 측정값을 FCC로 전송하여 중앙집중식 상태추정(Centralized State Estimation)을 수행한다. 하이브리드 아키텍처(Hybrid Architecture)는 원시 측정값과 독립적으로 계산된 자세 해를 모두 제공할 수 있다. 적절한 방식은 지연시간, 이중화, 연산 아키텍처, 검증 전략, 고장격리 및 요구되는 시스템 보증 수준에 따라 결정된다.

화물 UAV에서는 탑재화물의 변화가 진동, 구조 응답, 가속 특성 및 무게중심(Center of Gravity, CG) 위치의 변화를 통해 간접적으로 관성 상태추정에 영향을 줄 수 있다. IMU는 화물 특성을 직접 측정하는 것이 아니라 항공기의 운동을 측정하지만, 항공기 기준좌표계 및 회전중심에 대한 IMU의 설치 위치는 관측되는 가속도에 영향을 미친다. 탑재중량이 증가하고 항공기가 더욱 넓은 적재조건에서 운용될수록 정확한 구성정보(Configuration Information)의 중요성이 커진다.

초기화(Initialization)는 AHRS의 중요한 운용 단계이다. 능동 비행을 시작하기 전에 시스템은 센서 상태, 초기 자세, 바이어스 추정값, 타이밍 상태 및 외부 기준정보의 가용성을 확립해야 한다. 운용 조건이 허용되는 경우 정지 정렬(Stationary Alignment)을 통해 초기 바이어스와 자세 추정 정확도를 향상시킬 수 있다. FCC는 전원 인가 직후부터 유효한 자세 정보가 존재한다고 가정해서는 안 되며, 준비상태 로직(Readiness Logic)은 단순한 센서 통신 가능 상태와 완전히 수렴된 항법 해(Navigation Solution)를 구분해야 한다.

검증(Verification)은 센서 수준, 추정기 수준 및 항공기 수준의 시험을 포함해야 한다. 기록된 데이터와 시뮬레이션을 이용해 센서융합 알고리즘을 평가하고, 하드웨어 인더 루프(Hardware-in-the-Loop, HIL) 시험에서는 실제 운동 프로파일을 재현하면서 타이밍 오류, 센서 바이어스, 노이즈, 데이터 손실 및 고장을 주입할 수 있다. 지상시험에서는 진동과 전자기적 영향을 평가하고, 비행시험에서는 실제 동적 환경에서의 성능을 확인한다. 정상, 성능저하 및 중복 센싱 구성 사이의 전환을 특히 중요하게 검증해야 한다.

화물 UAV 아키텍처(Cargo UAV Architecture)에서 IMU와 AHRS 통합은 궁극적으로 비행제어가 의존하는 신뢰할 수 있는 동적 상태(Trusted Dynamic State)를 제공한다. 이 기능의 품질은 센서 자체의 사양뿐 아니라 보정, 장착, 좌표변환, 시간동기화, 필터링, 이중화, 고장관리 및 상태추정기 설계에 의해 결정된다. 견고한 통합 아키텍처는 FCC가 안정적이고 예측 가능한 제어를 유지하도록 하며, 2.5톤, 5톤 및 향후 10톤급 화물 UAV 플랫폼으로 확장되는 고도화된 자율운항을 지원한다.

##  

## 04.03. Autopilot Architecture

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

Autopilot architecture defines how sensing, state estimation, guidance, navigation, flight control, mode management, and actuator command generation are organized into a coordinated system that can fly a UAV with limited or no continuous human control. In a cargo UAV, the autopilot is not a single algorithm but a layered control architecture connecting mission objectives to deterministic aircraft behavior while maintaining defined operational and safety constraints.

At the lowest functional level, the autopilot depends on reliable aircraft-state information. IMUs, AHRS, GNSS receivers, air-data sensors, magnetometers, radar or laser altimeters, propulsion feedback, and actuator sensors provide measurements describing vehicle motion and system condition. These inputs are validated and fused before control decisions are generated, preventing individual raw measurements from directly determining safety-critical aircraft responses.

State estimation transforms sensor measurements into a coherent representation of aircraft position, velocity, attitude, angular rates, altitude, and other dynamic variables. The estimator must accommodate sensors operating at different update rates and with different uncertainty characteristics. High-rate inertial information supports rapid control response, while GNSS and other external references constrain accumulated drift and improve long-term navigation accuracy.

The stabilization layer forms the innermost part of the autopilot control hierarchy. Fast feedback loops regulate angular rates and aircraft attitude so that disturbances caused by wind, propulsion variation, structural motion, or control inputs do not destabilize the vehicle. These loops typically operate at substantially higher frequencies than mission-planning functions because aircraft stability depends on timely and predictable correction of dynamic errors.

Above stabilization, guidance functions determine how the aircraft should move to satisfy navigation and mission objectives. Guidance may generate desired attitude, heading, altitude, vertical speed, airspeed, ground speed, or trajectory references. Rather than commanding actuators directly, higher-level functions normally provide references to lower-level controllers, creating a hierarchy in which each layer operates within clearly defined authority and dynamic limits.

Navigation determines where the aircraft is and how it is moving relative to the intended route. Position and velocity information from GNSS can be combined with inertial navigation and other measurements to maintain a continuous navigation solution. Waypoints, routes, corridors, approach paths, landing locations, and geofencing constraints can then be represented within a common reference framework used by guidance and mission-management functions.

Flight-mode management coordinates the behavior of the complete autopilot. A cargo UAV may require ground, takeoff, climb, cruise, descent, approach, landing, hover, transition, return-to-home, emergency, and degraded-operation modes depending on its configuration. Each mode activates appropriate guidance logic, control laws, limits, and monitoring functions. Mode transitions must satisfy explicit conditions so that an unintended command cannot abruptly place the aircraft in an incompatible control state.

For eVTOL or hybrid cargo UAVs, transition management can become one of the most demanding autopilot functions. Hover, conversion, and wing-borne flight may involve substantially different aerodynamic behavior, actuator effectiveness, propulsion distribution, and control authority. The autopilot must coordinate these changes while preserving stability and trajectory continuity, often scheduling control parameters according to airspeed, configuration, propulsion state, or transition progress.

Control allocation translates desired forces and moments into commands for the available aircraft effectors. A conventional fixed-wing UAV may use elevators, ailerons, rudders, throttles, and related surfaces, while an eVTOL platform may coordinate multiple electric motors, variable-pitch rotors, tilting propulsion units, and aerodynamic surfaces. Allocation logic must respect actuator limits while distributing control effort according to the current flight configuration and available hardware.

Actuator commands are subject to physical and safety constraints before transmission. Position limits, rate limits, thrust limits, saturation handling, command validity checks, and feedback monitoring prevent calculated demands from exceeding available system capability. When an actuator or propulsion unit becomes unavailable, a fault-tolerant architecture may redistribute control effort among remaining effectors if sufficient control authority exists.

Cargo loading introduces additional variables into autopilot operation. Gross weight, center of gravity, inertia, and aerodynamic characteristics may change significantly between missions or during cargo handling. Validated loading information can therefore influence control gains, flight-envelope limits, takeoff and landing parameters, energy planning, and performance calculations. The autopilot should ensure that commanded maneuvers remain appropriate for the current aircraft mass configuration.

Mission management occupies a higher architectural layer than basic stabilization and control. It interprets mission plans containing routes, waypoints, altitude profiles, cargo destinations, operating zones, and contingency procedures. The mission manager determines the next operational objective, while guidance and flight-control layers determine how to achieve it. This separation allows mission logic to change without directly modifying the fundamental mechanisms that maintain aircraft stability.

Autonomous functions can extend this hierarchy with perception, obstacle avoidance, dynamic route planning, landing-zone assessment, weather response, or fleet-level coordination. However, high-level autonomy should operate through controlled interfaces rather than directly manipulating actuators. The deterministic autopilot retains responsibility for aircraft stabilization and flight-envelope compliance, while autonomous systems request trajectories, modes, or other bounded objectives that can be validated before execution.

Human supervision remains important even when routine flight is autonomous. The Ground Control Station can upload mission plans, monitor aircraft state, authorize selected operations, modify permitted objectives, or initiate contingency procedures. Communication loss must not leave the autopilot without defined behavior. Depending on mission and regulatory requirements, the aircraft may continue a validated mission, hold, divert, return, land, or enter another predefined safe state.

Failsafe logic is therefore integrated across the autopilot architecture. Events such as GNSS degradation, communication loss, low energy, propulsion faults, sensor disagreement, actuator failures, excessive deviation, or flight-envelope violations can trigger predefined responses. Failsafe behavior should be state-dependent because the safest action during cruise may differ from the safest action during hover, transition, approach, or cargo loading operations.

Autopilot health monitoring continuously evaluates sensors, processors, communication interfaces, control loops, actuators, propulsion systems, and navigation quality. Monitoring functions detect stale data, excessive estimation uncertainty, control saturation, abnormal tracking errors, timing violations, and hardware failures. The system can then isolate faulty information, reconfigure available resources, reduce operational capability, or transition to a degraded control mode before a fault develops into loss of control.

Redundant autopilot architectures may use multiple FCC channels executing equivalent or independently monitored control functions. Dual or triple channels can compare state estimates, mode states, and calculated commands to identify disagreement. Effective redundancy also requires consideration of independent power, clocks, sensors, communication paths, and I/O resources, because several processors sharing the same failure source do not provide true fault tolerance.

Deterministic scheduling ensures that stabilization and other time-critical functions execute within known deadlines regardless of activity in higher-level software. Navigation, mission management, communication, logging, diagnostics, and autonomy may operate at different rates and criticality levels. Partitioning processor time and memory helps prevent a computationally intensive noncritical task from delaying the control loops required to maintain stable flight.

The autopilot communication architecture connects sensors, FCCs, propulsion controllers, actuator electronics, navigation equipment, cargo systems, and other avionics. Different interfaces may carry high-rate deterministic control data and lower-rate mission or diagnostic information. Message priority, latency, synchronization, integrity checking, timeout behavior, and fault containment must therefore be considered as part of the control-system design rather than as independent networking concerns.

Software architecture should maintain clear separation among hardware interfaces, sensor processing, state estimation, control laws, guidance, navigation, mode management, fault management, and mission functions. Defined interfaces improve traceability and verification while reducing unintended coupling. Safety-critical functions can be isolated from less critical services so that logging, user interfaces, payload applications, or advanced autonomy cannot interfere with deterministic flight-control execution.

Initialization establishes whether the autopilot is ready to assume control. Before flight, the system verifies processor health, software configuration, sensor availability, attitude and navigation validity, actuator status, propulsion readiness, energy condition, communication state, and required mission information. Arming logic should prevent flight initiation when essential prerequisites are not satisfied and should distinguish between equipment presence and genuinely valid operational data.

Verification progresses from individual algorithms toward complete aircraft behavior. Mathematical simulation evaluates control and guidance logic, software-in-the-loop testing examines implemented software, and hardware-in-the-loop testing introduces actual processors and interfaces. Fault injection can reproduce sensor failures, delayed messages, actuator faults, communication loss, and abnormal transitions before flight. Ground and flight tests then confirm integrated behavior under representative operational conditions.

For a scalable cargo UAV family, autopilot architecture should preserve common functional principles while allowing aircraft-specific control laws, actuator configurations, propulsion systems, performance limits, and redundancy strategies. A 2.5-ton platform may use a different physical implementation from a 5-ton or 10-ton aircraft, yet the layered relationship among sensing, estimation, guidance, control, safety, and mission management can remain consistent across the family.

Ultimately, autopilot architecture provides the structured path from mission intent to controlled aircraft motion. Sensors describe the vehicle and environment, estimation determines its dynamic state, navigation establishes its location, guidance determines the desired motion, control laws calculate required forces and moments, and control allocation commands the available effectors. Mode management, monitoring, redundancy, and failsafe mechanisms surround these functions so that increasingly autonomous cargo UAVs can operate predictably, safely, and systematically.

자동조종 아키텍처(Autopilot Architecture)는 센싱(Sensing), 상태추정(State Estimation), 유도(Guidance), 항법(Navigation), 비행제어(Flight Control), 모드관리(Mode Management) 및 액추에이터 명령 생성(Actuator Command Generation)을 어떻게 하나의 조정된 시스템으로 구성하여, 지속적인 사람의 조작을 최소화하거나 전혀 없이 UAV를 비행시킬 것인지를 정의한다. 화물 UAV에서 자동조종장치(Autopilot)는 하나의 알고리즘이 아니라 임무 목표를 결정론적인 항공기 동작으로 연결하면서 정의된 운용 및 안전 제약조건을 유지하는 계층형 제어 아키텍처(Layered Control Architecture)이다.

가장 낮은 기능 계층에서 자동조종장치는 신뢰할 수 있는 항공기 상태정보(Aircraft-State Information)에 의존한다. IMU, AHRS, GNSS 수신기, 대기자료센서(Air-Data Sensor), 자력계(Magnetometer), 레이더 또는 레이저 고도계, 추진시스템 피드백 및 액추에이터 센서는 항공기의 운동과 시스템 상태를 나타내는 측정값을 제공한다. 이러한 입력은 제어결정을 생성하기 전에 검증되고 융합되어, 개별 원시 측정값이 안전 중요 항공기 동작을 직접 결정하지 않도록 한다.

상태추정(State Estimation)은 센서 측정값을 항공기의 위치, 속도, 자세, 각속도, 고도 및 기타 동적 변수에 대한 일관된 표현으로 변환한다. 추정기는 서로 다른 갱신 주기와 불확실성 특성을 가진 센서들을 처리할 수 있어야 한다. 고속 관성정보는 빠른 제어응답을 지원하고, GNSS 및 기타 외부 기준정보는 누적되는 드리프트(Drift)를 제한하여 장기적인 항법 정확도를 향상시킨다.

안정화 계층(Stabilization Layer)은 자동조종 제어계층의 가장 내부에 위치한다. 고속 피드백 루프(Fast Feedback Loop)는 각속도와 항공기 자세를 제어하여 바람, 추진력 변화, 구조적 운동 또는 제어입력으로 발생하는 외란이 항공기를 불안정하게 만들지 않도록 한다. 항공기 안정성은 동적 오차를 적시에 예측 가능하게 보정하는 것에 의존하기 때문에 이러한 루프는 일반적으로 임무계획 기능보다 훨씬 높은 주파수로 동작한다.

안정화 계층의 상위에서는 유도 기능(Guidance Function)이 항법 및 임무 목표를 만족하기 위해 항공기가 어떻게 움직여야 하는지를 결정한다. 유도 기능은 요구 자세, 방위, 고도, 수직속도, 대기속도, 지상속도 또는 궤적 기준값을 생성할 수 있다. 상위 기능은 액추에이터를 직접 명령하기보다는 일반적으로 하위 제어기에 기준값을 제공하며, 이를 통해 각 계층이 명확하게 정의된 제어 권한과 동적 한계 내에서 동작하는 계층구조를 형성한다.

항법(Navigation)은 항공기가 목표 경로에 대해 어디에 위치하며 어떻게 이동하고 있는지를 결정한다. GNSS의 위치 및 속도 정보는 관성항법(Inertial Navigation)과 기타 측정값을 결합하여 연속적인 항법 해(Navigation Solution)를 유지할 수 있다. 웨이포인트(Waypoint), 경로(Route), 비행회랑(Corridor), 접근경로, 착륙지점 및 지오펜싱(Geofencing) 제약조건은 유도와 임무관리 기능이 사용하는 공통 기준좌표계 안에서 표현될 수 있다.

비행모드관리(Flight-Mode Management)는 전체 자동조종장치의 동작을 조정한다. 화물 UAV는 구성에 따라 지상, 이륙, 상승, 순항, 하강, 접근, 착륙, 호버링(Hover), 전환비행(Transition), 자동귀환(Return-to-Home), 비상 및 성능저하 운용(Degraded Operation) 모드를 요구할 수 있다. 각 모드는 적절한 유도 로직, 제어법칙(Control Law), 제한조건 및 감시기능을 활성화한다. 의도하지 않은 명령이 항공기를 갑자기 부적절한 제어상태로 전환하지 않도록 모드 전환은 명확한 조건을 충족해야 한다.

eVTOL 또는 하이브리드 화물 UAV에서 전환관리(Transition Management)는 자동조종장치의 가장 까다로운 기능 중 하나가 될 수 있다. 호버링, 전환 및 주익양력 비행(Wing-Borne Flight)은 공력 특성, 액추에이터 효과, 추진력 분배 및 제어 권한에서 상당한 차이를 보일 수 있다. 자동조종장치는 안정성과 궤적 연속성을 유지하면서 이러한 변화를 조정해야 하며, 대기속도, 항공기 구성, 추진상태 또는 전환 진행도에 따라 제어 파라미터를 스케줄링할 수 있다.

제어할당(Control Allocation)은 요구되는 힘과 모멘트를 사용 가능한 항공기 제어효과기(Effector)의 명령으로 변환한다. 전통적인 고정익 UAV는 엘리베이터(Elevator), 에일러론(Aileron), 러더(Rudder), 스로틀(Throttle) 및 관련 조종면을 사용할 수 있으며, eVTOL 플랫폼은 여러 전기모터, 가변피치 로터(Variable-Pitch Rotor), 틸팅 추진장치(Tilting Propulsion Unit) 및 공력 조종면을 함께 제어할 수 있다. 제어할당 로직은 액추에이터 한계를 준수하면서 현재 비행 구성과 사용 가능한 하드웨어에 따라 제어력을 분배해야 한다.

액추에이터 명령(Actuator Command)은 전송되기 전에 물리적 제약조건과 안전 제한을 적용받는다. 위치 제한, 변화율 제한(Rate Limit), 추력 제한, 포화 처리(Saturation Handling), 명령 유효성 검사 및 피드백 감시는 계산된 요구값이 시스템의 실제 능력을 초과하지 않도록 한다. 액추에이터나 추진장치를 사용할 수 없게 된 경우 충분한 제어 권한이 남아 있다면 내고장성 아키텍처(Fault-Tolerant Architecture)는 남은 제어효과기 사이에서 제어력을 재분배할 수 있다.

화물 적재(Cargo Loading)는 자동조종 운용에 추가적인 변수를 발생시킨다. 총중량(Gross Weight), 무게중심(Center of Gravity, CG), 관성(Inertia) 및 공력 특성은 임무마다 또는 화물 취급 과정에서 크게 달라질 수 있다. 따라서 검증된 적재정보는 제어게인(Control Gain), 비행영역 제한(Flight-Envelope Limit), 이착륙 파라미터, 에너지 계획 및 성능 계산에 영향을 줄 수 있다. 자동조종장치는 명령된 기동이 현재 항공기의 질량 구성에 적합한지 보장해야 한다.

임무관리(Mission Management)는 기본적인 안정화 및 제어보다 상위 아키텍처 계층에 위치한다. 임무관리 기능은 경로, 웨이포인트, 고도 프로파일, 화물 목적지, 운용구역 및 비상절차가 포함된 임무계획을 해석한다. 임무관리자는 다음 운용 목표를 결정하고, 유도 및 비행제어 계층은 그 목표를 어떻게 달성할 것인지를 결정한다. 이러한 분리를 통해 항공기 안정성을 유지하는 기본 메커니즘을 직접 변경하지 않고도 임무 로직을 변경할 수 있다.

자율기능(Autonomous Function)은 인지(Perception), 장애물 회피, 동적 경로계획(Dynamic Route Planning), 착륙지역 평가, 기상 대응 또는 플릿 수준 협조(Fleet-Level Coordination)를 추가하여 이러한 계층구조를 확장할 수 있다. 그러나 상위 수준 자율기능은 액추에이터를 직접 조작하지 않고 제어된 인터페이스를 통해 동작해야 한다. 결정론적 자동조종장치는 항공기 안정화와 비행영역 준수에 대한 책임을 유지하며, 자율시스템은 실행 전에 검증할 수 있는 궤적, 모드 또는 제한된 목표를 요청한다.

일상적인 비행이 자율적으로 수행되더라도 사람의 감독(Human Supervision)은 여전히 중요하다. 지상통제소(Ground Control Station, GCS)는 임무계획을 업로드하고 항공기 상태를 감시하며 특정 운용을 승인하고 허용된 목표를 수정하거나 비상절차를 시작할 수 있다. 통신이 두절되더라도 자동조종장치에는 정의된 동작이 존재해야 한다. 임무와 규제 요구사항에 따라 항공기는 검증된 임무를 계속하거나 대기, 우회, 귀환, 착륙 또는 다른 사전 정의된 안전상태로 전환할 수 있다.

따라서 비상안전 로직(Failsafe Logic)은 자동조종 아키텍처 전반에 통합된다. GNSS 성능저하, 통신 두절, 에너지 부족, 추진시스템 고장, 센서 불일치, 액추에이터 고장, 과도한 경로 이탈 또는 비행영역 위반과 같은 사건은 사전에 정의된 대응을 유발할 수 있다. 순항 중 가장 안전한 대응이 호버링, 전환비행, 접근 또는 화물 적재 운용 중의 가장 안전한 대응과 다를 수 있으므로 비상안전 동작은 항공기 상태에 따라 달라져야 한다.

자동조종 상태감시(Autopilot Health Monitoring)는 센서, 프로세서, 통신 인터페이스, 제어루프, 액추에이터, 추진시스템 및 항법 품질을 지속적으로 평가한다. 감시기능은 오래된 데이터(Stale Data), 과도한 상태추정 불확실성, 제어 포화, 비정상적인 추종오차(Tracking Error), 타이밍 위반 및 하드웨어 고장을 검출한다. 시스템은 고장이 제어상실로 발전하기 전에 잘못된 정보를 격리하고 사용 가능한 자원을 재구성하거나 운용능력을 제한하고 성능저하 제어모드로 전환할 수 있다.

중복 자동조종 아키텍처(Redundant Autopilot Architecture)는 동일하거나 독립적으로 감시되는 제어기능을 수행하는 여러 FCC 채널을 사용할 수 있다. 이중 또는 삼중 채널은 상태추정값, 모드 상태 및 계산된 명령을 비교하여 불일치를 식별할 수 있다. 효과적인 이중화를 위해서는 독립적인 전원, 클록, 센서, 통신 경로 및 입출력 자원도 고려해야 한다. 여러 프로세서가 동일한 고장 원인을 공유한다면 진정한 내고장성을 제공할 수 없기 때문이다.

결정론적 스케줄링(Deterministic Scheduling)은 상위 수준 소프트웨어의 동작과 관계없이 안정화 및 기타 시간 임계 기능이 정해진 마감시간 안에 실행되도록 보장한다. 항법, 임무관리, 통신, 로깅, 진단 및 자율기능은 서로 다른 주기와 중요도로 동작할 수 있다. 프로세서 시간과 메모리를 파티셔닝(Partitioning)하면 연산량이 많은 비핵심 작업이 안정적인 비행 유지에 필요한 제어루프 실행을 지연시키는 것을 방지할 수 있다.

자동조종 통신 아키텍처(Autopilot Communication Architecture)는 센서, FCC, 추진제어기, 액추에이터 전자장치, 항법장비, 화물시스템 및 기타 항공전자 장비를 연결한다. 서로 다른 인터페이스를 통해 고속 결정론적 제어데이터와 상대적으로 낮은 주기의 임무 또는 진단정보를 전달할 수 있다. 따라서 메시지 우선순위, 지연시간, 동기화, 무결성 검사, 타임아웃 동작 및 고장격리(Fault Containment)를 독립적인 네트워크 문제가 아니라 제어시스템 설계의 일부로 고려해야 한다.

소프트웨어 아키텍처(Software Architecture)는 하드웨어 인터페이스, 센서 처리, 상태추정, 제어법칙, 유도, 항법, 모드관리, 고장관리 및 임무기능 사이를 명확하게 분리해야 한다. 정의된 인터페이스는 의도하지 않은 결합을 줄이면서 추적성(Traceability)과 검증을 향상시킨다. 안전 중요 기능은 상대적으로 중요도가 낮은 서비스와 격리하여 로깅, 사용자 인터페이스, 탑재 응용프로그램 또는 고급 자율기능이 결정론적 비행제어 실행을 방해하지 않도록 할 수 있다.

초기화(Initialization)는 자동조종장치가 제어를 담당할 준비가 되었는지를 확립하는 과정이다. 비행 전에 시스템은 프로세서 상태, 소프트웨어 구성, 센서 가용성, 자세 및 항법 유효성, 액추에이터 상태, 추진시스템 준비상태, 에너지 상태, 통신 상태 및 필요한 임무정보를 확인한다. 무장 로직(Arming Logic)은 필수 선행조건이 충족되지 않은 상태에서 비행이 시작되지 않도록 해야 하며, 단순한 장비 존재 여부와 실제로 유효한 운용 데이터를 구분해야 한다.

검증(Verification)은 개별 알고리즘에서 완전한 항공기 동작으로 단계적으로 확장된다. 수학적 시뮬레이션은 제어 및 유도 로직을 평가하고, 소프트웨어 인더 루프(Software-in-the-Loop, SIL) 시험은 구현된 소프트웨어를 검증하며, 하드웨어 인더 루프(Hardware-in-the-Loop, HIL) 시험은 실제 프로세서와 인터페이스를 포함한다. 비행 전에 고장주입(Fault Injection)을 통해 센서 고장, 메시지 지연, 액추에이터 고장, 통신 두절 및 비정상적인 모드 전환을 재현할 수 있다. 이후 지상시험과 비행시험을 통해 대표적인 운용조건에서 통합된 시스템 동작을 확인한다.

확장 가능한 화물 UAV 제품군(Scalable Cargo UAV Family)의 자동조종 아키텍처는 항공기별 제어법칙, 액추에이터 구성, 추진시스템, 성능 제한 및 이중화 전략의 차이를 허용하면서 공통적인 기능 원칙을 유지해야 한다. 2.5톤급 플랫폼은 5톤 또는 10톤급 항공기와 다른 물리적 구현을 사용할 수 있지만, 센싱, 상태추정, 유도, 제어, 안전 및 임무관리 사이의 계층적 관계는 전체 제품군에서 일관되게 유지할 수 있다.

궁극적으로 자동조종 아키텍처(Autopilot Architecture)는 임무 의도(Mission Intent)를 제어된 항공기 운동으로 변환하는 구조화된 경로를 제공한다. 센서는 항공기와 환경을 관측하고, 상태추정은 동적 상태를 결정하며, 항법은 현재 위치를 확립하고, 유도는 요구되는 운동을 결정하며, 제어법칙은 필요한 힘과 모멘트를 계산하고, 제어할당은 사용 가능한 제어효과기에 명령을 전달한다. 모드관리, 상태감시, 이중화 및 비상안전 메커니즘이 이러한 기능을 둘러싸고 작동함으로써 고도화되는 자율 화물 UAV가 예측 가능하고 안전하며 체계적으로 운용될 수 있도록 한다.

##  

## 04.04. Failsafe Design

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

Failsafe design defines how a UAV detects abnormal conditions, evaluates their severity, and transitions toward a controlled state when normal operation can no longer be guaranteed. In a cargo UAV, failsafe behavior must protect the aircraft, payload, people, and surrounding infrastructure without depending on continuous human intervention. It therefore combines fault detection, decision logic, degraded operation, redundancy, emergency modes, and predefined recovery actions within the flight control architecture.

A failsafe system begins with continuous monitoring of information required for safe flight. The Flight Control Computer (FCC) evaluates sensors, navigation quality, communication links, propulsion systems, actuators, electrical power, energy reserves, processor health, and flight-control performance. Monitoring is not limited to detecting complete equipment failure; gradual degradation, excessive uncertainty, delayed data, abnormal tracking error, or disagreement between redundant channels may also indicate that normal operation is becoming unsafe.

Fault detection must distinguish temporary disturbances from persistent failures. A single missing communication packet or short GNSS disturbance should not necessarily trigger an emergency landing, while sustained data loss may require immediate reconfiguration. Persistence timers, validity checks, confidence levels, hysteresis, and cross-comparison can prevent unnecessary mode transitions while ensuring that genuine faults are recognized before they develop into hazardous aircraft behavior.

Fault classification determines the appropriate response. Some faults can be tolerated without changing the mission, while others require reduced performance, route modification, return-to-home, diversion, controlled landing, or immediate emergency action. The failsafe architecture therefore considers both fault severity and available aircraft capability. A system should not execute the same response for every failure because the safest action depends on flight phase, vehicle configuration, environment, remaining energy, and available control authority.

Sensor failures are managed through validation, redundancy, and estimation. IMU, AHRS, GNSS, air-data, altitude, and other measurements can be checked for range, rate, freshness, consistency, and agreement with independent sources. When one sensor becomes unreliable, the estimator may reject it and continue using remaining valid information. The resulting navigation or control performance may be reduced, but controlled flight can continue when sufficient observability and sensor diversity remain available.

GNSS loss is particularly important for autonomous cargo UAVs because navigation, route tracking, geofencing, and landing functions may depend heavily on accurate position information. Temporary GNSS degradation can be bridged using inertial navigation and other available references, although position uncertainty grows over time. The failsafe logic must monitor this uncertainty and determine whether the aircraft can continue, hold, return, divert, or land before navigation accuracy becomes unacceptable.

Communication loss must also have explicitly defined behavior. Loss of the Ground Control Station link cannot leave the aircraft waiting indefinitely for operator commands. Depending on the approved mission concept, the UAV may continue along a validated route, enter a holding pattern, return to a predefined recovery location, divert to an alternate site, or execute a controlled landing. The selected action should consider remaining energy, airspace constraints, weather, terrain, and navigation capability.

Propulsion faults can rapidly reduce available flight capability, especially in eVTOL and distributed-propulsion aircraft. The flight controller must identify abnormal thrust, motor speed, temperature, current, vibration, or propulsion-controller status and determine whether sufficient remaining propulsion exists. Control allocation can redistribute thrust among healthy units where the configuration permits, while flight-envelope limits may be reduced to prevent commands that exceed degraded propulsion capability.

Actuator failures require similar reconfiguration. A control surface, servo, tilt mechanism, or other effector may become unavailable, move slowly, become stuck, or disagree with its commanded position. Feedback monitoring allows the FCC to compare requested and actual behavior. If sufficient redundant control authority remains, the control allocator can compensate using other effectors. Otherwise, the system must transition toward an emergency condition compatible with the remaining controllability.

Electrical power failures require coordinated response because avionics, sensors, actuators, communication equipment, and propulsion-support systems may depend on different power domains. Independent power sources and essential buses can prevent a single electrical fault from disabling the complete flight-control system. When power becomes limited, load shedding can disconnect nonessential equipment so that critical sensing, computation, communication, and control functions remain operational for as long as necessary.

Low-energy conditions are different from sudden power failures and should be predicted before they become emergencies. The aircraft can continuously estimate remaining battery energy, fuel, hybrid-system capability, mission distance, reserve requirements, and expected landing demand. Failsafe logic can progressively restrict mission options as energy margin decreases, initiating return or diversion while sufficient reserve remains instead of waiting until propulsion capability becomes critically limited.

Flight-envelope protection prevents commands or disturbances from driving the aircraft beyond validated operating boundaries. Airspeed, attitude, angular rate, load factor, altitude, descent rate, thrust demand, battery condition, and other parameters may be monitored according to aircraft configuration. When limits are approached, the autopilot can constrain commands or prioritize recovery. Envelope protection remains important even when the original unsafe request originates from mission autonomy or a remote operator.

Failsafe behavior must be aware of the current flight mode. A propulsion fault during cruise may permit diversion to an alternate landing site, whereas the same fault during hover or transition may require a much faster response. Similarly, GNSS loss during high-altitude cruise differs from loss during precision landing. State-dependent logic therefore combines detected faults with flight phase, altitude, speed, configuration, terrain, and available recovery options before selecting an action.

Degraded operation is often preferable to immediate mission termination. If one sensor, communication path, FCC channel, or actuator fails but sufficient capability remains, the aircraft can enter a degraded mode with reduced speed, maneuver limits, autonomy, or mission scope. This approach preserves controlled operation while explicitly acknowledging reduced system capability. Degraded modes must be predefined and verified rather than improvised dynamically after a failure occurs.

Redundancy supports failsafe design by providing alternative resources after failures. Dual or triple FCCs, multiple IMUs, independent power domains, redundant communication links, and distributed propulsion can increase fault tolerance. However, redundancy must address common-cause failures. Identical channels sharing the same power supply, network, software dependency, cooling path, or environmental vulnerability may fail together and therefore provide less protection than their component count suggests.

Voting and cross-monitoring mechanisms help determine which redundant channel remains trustworthy. Multiple FCCs can compare state estimates, mode states, health information, and actuator commands. When disagreement occurs, the architecture must determine whether a faulty channel can be isolated reliably. Triple-channel systems can support majority voting in selected functions, while dual-channel architectures may require independent monitors or additional evidence because simple disagreement does not identify which channel is correct.

Failsafe mode transitions must themselves be safe. Rapid switching between normal and emergency states can create unstable behavior if thresholds fluctuate around a boundary. Transition logic therefore uses controlled entry conditions, persistence requirements, hysteresis, and clearly defined recovery criteria. Some emergency states may intentionally be latched so that normal operation cannot resume automatically until the underlying condition has been verified or appropriate operator authorization has been received.

Return-to-home is useful but should not be treated as a universal failsafe solution. Returning may be inappropriate when navigation is unreliable, energy is insufficient, severe weather blocks the route, propulsion capability is degraded, or the original home location is no longer safe. A robust cargo UAV architecture can maintain several recovery alternatives, including holding areas, diversion airports, emergency landing zones, or mission-specific safe locations, and select among them according to current conditions.

Emergency landing logic must balance aircraft controllability with risks on the ground. The system may evaluate reachable landing locations using altitude, energy, glide or powered-flight capability, terrain, obstacles, and available navigation information. For highly autonomous aircraft, perception systems may assist landing-zone assessment, but safety-critical execution should remain bounded by validated flight-control constraints. The objective is a controlled termination of flight rather than simply stopping the mission.

Cargo characteristics can influence failsafe decisions. A heavily loaded aircraft may have different glide performance, hover endurance, landing distance, structural limits, and energy requirements from an unloaded vehicle. Center-of-gravity location and payload security may further restrict emergency maneuvers. Failsafe logic should therefore use validated aircraft configuration and cargo information when determining achievable recovery trajectories, allowable accelerations, and suitable landing strategies.

Human interaction must remain clearly defined during emergencies. The Ground Control Station should present fault status, aircraft capability, selected failsafe mode, and relevant recovery information without requiring the operator to diagnose every low-level failure. Operator commands may modify or authorize selected actions where permitted, but the aircraft must retain autonomous protection against unsafe commands, excessive delay, or complete communication loss during time-critical events.

Failsafe software should be separated appropriately from noncritical mission and payload applications. Fault monitors, safety state machines, command validation, envelope protection, and essential recovery logic require deterministic execution and controlled interfaces. A computationally intensive perception task, cargo application, logging process, or user-interface function should not prevent emergency logic from executing within its required deadline. Architectural partitioning therefore contributes directly to fault containment.

Verification of failsafe behavior requires systematic fault injection rather than testing only normal flight. Simulation, software-in-the-loop, and hardware-in-the-loop environments can introduce sensor bias, GNSS loss, communication interruption, actuator faults, propulsion degradation, processor resets, power failures, and timing errors. Tests should examine not only whether a fault is detected but also whether classification, transition, reconfiguration, recovery, and eventual restoration behave correctly.

Ground and flight testing progressively validate failsafe responses under realistic dynamics and environmental conditions. Individual failures are introduced only within carefully controlled test boundaries, while combinations of faults are analyzed according to system safety requirements. Particular attention is required at mode transitions such as takeoff, hover-to-cruise conversion, approach, and landing because available recovery time and control authority may be substantially lower than during steady cruise.

For a scalable cargo UAV family, failsafe philosophy can remain consistent while recovery strategies evolve with aircraft size and configuration. A 2.5-ton, 5-ton, and future 10-ton aircraft may differ significantly in propulsion redundancy, energy architecture, landing capability, operational airspace, and consequence of failure. Larger platforms therefore require increasingly rigorous fault containment, redundancy management, emergency planning, verification, and system-level assurance.

Ultimately, failsafe design converts abnormal conditions from uncontrolled surprises into predefined system states and responses. Detection identifies what has changed, classification determines its significance, redundancy preserves available capability, degraded modes limit exposure, and recovery logic directs the aircraft toward the safest achievable outcome. Integrated with the FCC, autopilot, propulsion, power, navigation, communication, and cargo systems, this architecture provides a fundamental safety foundation for autonomous cargo UAV operation.

비상안전설계(Failsafe Design)는 UAV가 비정상 상태를 감지하고 그 심각도를 평가하며 정상 운용을 더 이상 보장할 수 없을 때 제어 가능한 상태로 전환하는 방법을 정의한다. 화물 UAV에서 비상안전 동작(Failsafe Behavior)은 지속적인 사람의 개입에 의존하지 않으면서 항공기, 탑재화물, 사람 및 주변 인프라를 보호해야 한다. 따라서 비행제어 아키텍처 내에서 고장검출(Fault Detection), 의사결정 로직, 성능저하 운용(Degraded Operation), 이중화(Redundancy), 비상모드 및 사전에 정의된 복구동작을 통합한다.

비상안전시스템(Failsafe System)은 안전한 비행에 필요한 정보를 지속적으로 감시하는 것에서 시작한다. 비행제어컴퓨터(Flight Control Computer, FCC)는 센서, 항법 품질, 통신 링크, 추진시스템, 액추에이터, 전력시스템, 에너지 잔량, 프로세서 상태 및 비행제어 성능을 평가한다. 감시는 장비의 완전한 고장만을 검출하는 데 한정되지 않으며, 점진적인 성능저하, 과도한 불확실성, 데이터 지연, 비정상적인 추종오차 또는 중복 채널 간의 불일치 역시 정상 운용이 불안전해지고 있음을 나타낼 수 있다.

고장검출(Fault Detection)은 일시적인 외란과 지속적인 고장을 구분해야 한다. 단일 통신 패킷 손실이나 짧은 GNSS 장애가 반드시 비상착륙을 유발할 필요는 없지만, 지속적인 데이터 손실은 즉각적인 시스템 재구성을 요구할 수 있다. 지속시간 타이머(Persistence Timer), 유효성 검사, 신뢰도 수준, 히스테리시스(Hysteresis) 및 상호비교(Cross-Comparison)를 사용하면 불필요한 모드 전환을 방지하면서 실제 고장이 위험한 항공기 동작으로 발전하기 전에 이를 식별할 수 있다.

고장분류(Fault Classification)는 적절한 대응을 결정한다. 일부 고장은 임무를 변경하지 않고 허용할 수 있지만, 다른 고장은 성능 제한, 경로 변경, 자동귀환(Return-to-Home), 우회, 제어착륙 또는 즉각적인 비상조치를 요구할 수 있다. 따라서 비상안전 아키텍처는 고장의 심각도와 현재 사용 가능한 항공기 능력을 함께 고려한다. 가장 안전한 대응은 비행 단계, 항공기 구성, 환경, 잔여 에너지 및 사용 가능한 제어 권한에 따라 달라지므로 모든 고장에 동일한 대응을 적용해서는 안 된다.

센서 고장(Sensor Failure)은 검증, 이중화 및 상태추정을 통해 관리한다. IMU, AHRS, GNSS, 대기자료, 고도 및 기타 측정값은 범위, 변화율, 최신성(Freshness), 일관성 및 독립적인 정보원과의 일치 여부를 기준으로 검사할 수 있다. 하나의 센서가 신뢰할 수 없게 되면 추정기는 해당 정보를 배제하고 나머지 유효한 정보를 사용하여 계속 동작할 수 있다. 항법 또는 제어 성능은 저하될 수 있지만 충분한 관측가능성(Observability)과 센서 다양성이 유지된다면 제어 가능한 비행을 지속할 수 있다.

GNSS 손실은 항법, 경로 추종, 지오펜싱(Geofencing) 및 착륙 기능이 정확한 위치정보에 크게 의존할 수 있는 자율 화물 UAV에서 특히 중요하다. 일시적인 GNSS 성능저하는 관성항법(Inertial Navigation)과 기타 사용 가능한 기준정보를 이용하여 보완할 수 있지만 시간이 지남에 따라 위치 불확실성이 증가한다. 비상안전 로직은 이러한 불확실성을 지속적으로 감시하여 항법 정확도가 허용할 수 없는 수준으로 저하되기 전에 비행 지속, 대기, 귀환, 우회 또는 착륙 여부를 결정해야 한다.

통신 두절(Communication Loss) 역시 명확하게 정의된 동작을 가져야 한다. 지상통제소(Ground Control Station, GCS)와의 통신이 끊어졌다고 해서 항공기가 운용자의 명령을 무기한 기다려서는 안 된다. 승인된 임무 개념에 따라 UAV는 검증된 경로를 계속 비행하거나 대기패턴(Holding Pattern)에 진입하고, 사전에 정의된 복구지점으로 귀환하거나 대체 지점으로 우회하거나 제어착륙을 수행할 수 있다. 선택되는 동작은 잔여 에너지, 공역 제약, 기상, 지형 및 항법 능력을 고려해야 한다.

추진시스템 고장(Propulsion Fault)은 특히 eVTOL 및 분산추진(Distributed Propulsion) 항공기에서 사용 가능한 비행 능력을 빠르게 감소시킬 수 있다. 비행제어기는 비정상적인 추력, 모터 회전속도, 온도, 전류, 진동 또는 추진제어기 상태를 식별하고 잔여 추진력으로 비행을 유지할 수 있는지를 판단해야 한다. 항공기 구성이 허용하는 경우 제어할당(Control Allocation)을 통해 정상 추진장치 사이에서 추력을 재분배할 수 있으며, 성능저하된 추진 능력을 초과하는 명령을 방지하기 위해 비행영역 제한을 축소할 수 있다.

액추에이터 고장(Actuator Failure) 역시 유사한 재구성을 요구한다. 조종면(Control Surface), 서보(Servo), 틸트 메커니즘(Tilt Mechanism) 또는 기타 제어효과기(Effector)는 사용 불능, 느린 동작, 고착 또는 명령 위치와 실제 위치가 불일치하는 상태가 될 수 있다. 피드백 감시를 통해 FCC는 요구된 동작과 실제 동작을 비교할 수 있다. 충분한 중복 제어 권한이 남아 있다면 제어할당기는 다른 제어효과기를 이용하여 보상할 수 있으며, 그렇지 않다면 남아 있는 조종 가능성(Controllability)에 적합한 비상상태로 전환해야 한다.

전력시스템 고장(Electrical Power Failure)은 항공전자, 센서, 액추에이터, 통신장비 및 추진지원시스템이 서로 다른 전원 도메인(Power Domain)에 의존할 수 있기 때문에 통합된 대응이 필요하다. 독립적인 전원과 필수 버스(Essential Bus)를 사용하면 하나의 전기적 고장이 전체 비행제어시스템을 무력화하는 것을 방지할 수 있다. 사용 가능한 전력이 제한될 경우 부하차단(Load Shedding)을 통해 비필수 장비를 분리하여 중요한 센싱, 연산, 통신 및 제어 기능을 필요한 시간 동안 유지할 수 있다.

저에너지 상태(Low-Energy Condition)는 갑작스러운 전원 고장과 다르며 비상상태가 되기 전에 예측해야 한다. 항공기는 잔여 배터리 에너지, 연료, 하이브리드시스템 능력, 임무 거리, 예비 에너지 요구량 및 예상 착륙 소요량을 지속적으로 추정할 수 있다. 비상안전 로직은 추진 능력이 임계 수준까지 저하될 때까지 기다리는 대신 에너지 여유가 감소함에 따라 임무 선택지를 단계적으로 제한하고 충분한 예비량이 남아 있을 때 귀환이나 우회를 시작할 수 있다.

비행영역 보호(Flight-Envelope Protection)는 명령이나 외란으로 인해 항공기가 검증된 운용경계를 벗어나는 것을 방지한다. 대기속도, 자세, 각속도, 하중계수(Load Factor), 고도, 하강률, 추력 요구량, 배터리 상태 및 기타 파라미터를 항공기 구성에 따라 감시할 수 있다. 제한값에 접근하면 자동조종장치(Autopilot)는 명령을 제한하거나 복구동작을 우선할 수 있다. 원래의 위험한 명령이 임무 자율시스템이나 원격 운용자로부터 발생한 경우에도 비행영역 보호는 유지되어야 한다.

비상안전 동작은 현재 비행모드(Flight Mode)를 인식해야 한다. 순항 중 발생한 추진시스템 고장은 대체 착륙지점으로의 우회를 허용할 수 있지만, 호버링이나 전환비행 중 동일한 고장은 훨씬 빠른 대응을 요구할 수 있다. 마찬가지로 고고도 순항 중 GNSS 손실과 정밀착륙 중 GNSS 손실은 서로 다른 의미를 가진다. 따라서 상태의존 로직(State-Dependent Logic)은 고장정보와 비행 단계, 고도, 속도, 항공기 구성, 지형 및 사용 가능한 복구수단을 결합하여 대응동작을 선택한다.

성능저하 운용(Degraded Operation)은 즉각적인 임무 종료보다 더 적절한 경우가 많다. 하나의 센서, 통신 경로, FCC 채널 또는 액추에이터가 고장나더라도 충분한 능력이 남아 있다면 항공기는 속도, 기동한계, 자율성 또는 임무범위를 제한한 성능저하 모드(Degraded Mode)로 전환할 수 있다. 이러한 방식은 시스템 능력이 감소했음을 명확히 인정하면서 제어 가능한 운용을 유지한다. 성능저하 모드는 고장이 발생한 이후 즉흥적으로 결정하는 것이 아니라 사전에 정의하고 검증해야 한다.

이중화(Redundancy)는 고장 이후 사용할 수 있는 대체 자원을 제공함으로써 비상안전설계를 지원한다. 이중 또는 삼중 FCC, 다중 IMU, 독립적인 전원 도메인, 중복 통신 링크 및 분산추진시스템은 내고장성(Fault Tolerance)을 향상시킬 수 있다. 그러나 이중화는 공통원인고장(Common-Cause Failure)을 고려해야 한다. 동일한 전원공급장치, 네트워크, 소프트웨어 의존성, 냉각경로 또는 환경적 취약성을 공유하는 동일한 채널은 동시에 고장날 수 있으므로 단순한 구성요소 수보다 실제 독립성이 중요하다.

투표 및 상호감시 메커니즘(Voting and Cross-Monitoring Mechanism)은 중복 채널 가운데 어느 채널을 신뢰할 수 있는지 판단하는 데 도움을 준다. 여러 FCC는 상태추정값, 모드 상태, 상태정보 및 액추에이터 명령을 비교할 수 있다. 불일치가 발생하면 아키텍처는 고장 채널을 신뢰성 있게 격리할 수 있는지를 판단해야 한다. 삼중 채널 시스템은 특정 기능에서 다수결 투표(Majority Voting)를 지원할 수 있지만, 이중 채널에서는 단순한 불일치만으로 어느 채널이 올바른지 판단할 수 없으므로 독립적인 감시기 또는 추가적인 판단 근거가 필요할 수 있다.

비상안전 모드 전환(Failsafe Mode Transition) 자체도 안전해야 한다. 임계값 주변에서 상태가 반복적으로 변하면 정상상태와 비상상태 사이의 빠른 전환으로 불안정한 동작이 발생할 수 있다. 따라서 전환 로직은 제어된 진입조건, 지속시간 요구조건, 히스테리시스 및 명확하게 정의된 복귀조건을 사용한다. 일부 비상상태는 의도적으로 래치(Latch)하여 근본적인 문제가 검증되거나 적절한 운용자 승인이 이루어질 때까지 자동으로 정상운용에 복귀하지 못하도록 할 수 있다.

자동귀환(Return-to-Home)은 유용하지만 모든 상황에 적용되는 보편적인 비상안전 해결책으로 간주해서는 안 된다. 항법 신뢰성이 낮거나 에너지가 부족하거나 악천후가 귀환경로를 차단하거나 추진 능력이 저하되었거나 기존의 귀환지점이 더 이상 안전하지 않은 경우에는 귀환이 적절하지 않을 수 있다. 견고한 화물 UAV 아키텍처는 대기구역, 대체공항, 비상착륙구역 또는 임무별 안전지점과 같은 여러 복구대안을 유지하고 현재 상황에 따라 적절한 대안을 선택할 수 있어야 한다.

비상착륙 로직(Emergency Landing Logic)은 항공기의 조종 가능성과 지상 위험을 함께 고려해야 한다. 시스템은 고도, 에너지, 활공 또는 동력비행 능력, 지형, 장애물 및 사용 가능한 항법정보를 이용하여 도달 가능한 착륙지점을 평가할 수 있다. 고도로 자율화된 항공기에서는 인지시스템(Perception System)이 착륙지점 평가를 지원할 수 있지만, 안전 중요 실행은 검증된 비행제어 제약조건 내에서 이루어져야 한다. 목표는 단순한 임무 중단이 아니라 제어된 비행 종료(Controlled Termination of Flight)이다.

화물 특성(Cargo Characteristics)은 비상안전 의사결정에 영향을 줄 수 있다. 중량이 큰 항공기는 무적재 항공기와 비교하여 활공성능, 호버링 지속시간, 착륙거리, 구조적 한계 및 에너지 요구량이 달라질 수 있다. 무게중심 위치와 화물 고정 상태 역시 비상기동을 제한할 수 있다. 따라서 비상안전 로직은 달성 가능한 복구궤적, 허용가속도 및 적절한 착륙전략을 결정할 때 검증된 항공기 구성정보와 화물정보를 사용해야 한다.

비상상황에서 사람과 시스템의 상호작용(Human Interaction)은 명확하게 정의되어야 한다. 지상통제소는 운용자가 모든 저수준 고장을 직접 진단하지 않더라도 고장상태, 현재 항공기 능력, 선택된 비상안전 모드 및 관련 복구정보를 제공해야 한다. 허용되는 범위에서 운용자 명령이 특정 동작을 수정하거나 승인할 수 있지만, 항공기는 시간 임계 상황에서 위험한 명령, 과도한 지연 또는 완전한 통신 두절에 대해 자율적인 보호기능을 유지해야 한다.

비상안전 소프트웨어(Failsafe Software)는 중요도가 낮은 임무 및 탑재 응용프로그램과 적절하게 분리되어야 한다. 고장감시기, 안전 상태기계(Safety State Machine), 명령 검증, 비행영역 보호 및 필수 복구 로직은 결정론적 실행과 통제된 인터페이스를 필요로 한다. 연산량이 많은 인지 작업, 화물 응용프로그램, 로깅 프로세스 또는 사용자 인터페이스 기능이 비상 로직의 요구 마감시간 내 실행을 방해해서는 안 된다. 따라서 아키텍처 파티셔닝(Architectural Partitioning)은 고장격리(Fault Containment)에 직접적으로 기여한다.

비상안전 동작의 검증(Verification)은 정상비행만 시험하는 것이 아니라 체계적인 고장주입(Fault Injection)을 요구한다. 시뮬레이션, 소프트웨어 인더 루프(Software-in-the-Loop, SIL) 및 하드웨어 인더 루프(Hardware-in-the-Loop, HIL) 환경에서는 센서 바이어스, GNSS 손실, 통신 중단, 액추에이터 고장, 추진 성능저하, 프로세서 리셋, 전원 고장 및 타이밍 오류를 주입할 수 있다. 시험에서는 고장검출 여부뿐 아니라 분류, 전환, 재구성, 복구 및 최종적인 정상상태 복귀가 올바르게 이루어지는지도 검증해야 한다.

지상시험(Ground Test)과 비행시험(Flight Test)은 실제 동역학 및 환경조건에서 비상안전 대응을 단계적으로 검증한다. 개별 고장은 엄격하게 통제된 시험경계 안에서만 주입하며, 복합고장은 시스템 안전 요구사항에 따라 분석한다. 특히 이륙, 호버링에서 순항으로의 전환, 접근 및 착륙과 같은 모드 전환에서는 정상 순항보다 사용할 수 있는 복구시간과 제어 권한이 크게 감소할 수 있으므로 특별한 검증이 필요하다.

확장 가능한 화물 UAV 제품군(Scalable Cargo UAV Family)에서는 비상안전설계의 기본 철학을 일관되게 유지하면서 항공기 크기와 구성에 따라 복구전략을 발전시킬 수 있다. 2.5톤, 5톤 및 향후 10톤급 항공기는 추진 이중화, 에너지 아키텍처, 착륙 능력, 운용 공역 및 고장 결과 측면에서 상당한 차이가 있을 수 있다. 따라서 플랫폼이 대형화될수록 더욱 엄격한 고장격리, 이중화 관리, 비상계획, 검증 및 시스템 수준 보증(System-Level Assurance)이 요구된다.

궁극적으로 비상안전설계(Failsafe Design)는 비정상 상황을 통제되지 않은 돌발사건에서 사전에 정의된 시스템 상태와 대응으로 변환한다. 고장검출은 무엇이 변화했는지를 식별하고, 고장분류는 그 중요성을 결정하며, 이중화는 사용 가능한 능력을 유지하고, 성능저하 모드는 위험 노출을 제한하며, 복구 로직은 항공기를 달성 가능한 가장 안전한 결과로 유도한다. FCC, 자동조종장치, 추진시스템, 전력시스템, 항법, 통신 및 화물시스템과 통합된 이러한 아키텍처는 자율 화물 UAV 운용을 위한 핵심적인 안전 기반을 제공한다.

##  

## 04.05. Flight Control Redundancy

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

Flight control redundancy is the architectural principle of providing multiple independent sensing, computing, communication, power, and actuation resources so that a UAV can maintain controlled flight after selected failures. In a cargo UAV, redundancy must extend beyond duplicating the Flight Control Computer (FCC). The objective is to preserve sufficient control authority, state knowledge, and system integrity when individual components or complete control channels become unavailable.

A flight control channel typically includes sensor inputs, processing hardware, flight-control software, communication interfaces, power supplies, and connections to actuators or propulsion controllers. If several FCCs depend on the same IMU, power converter, network switch, or communication bus, failure of that shared resource can disable every channel simultaneously. Effective redundancy therefore begins by identifying complete functional paths rather than simply counting computers.

Dual-channel architectures provide two flight-control paths capable of cross-monitoring each other. Each channel can independently calculate aircraft state and control commands, allowing disagreements to be detected rapidly. However, disagreement between two channels does not inherently identify which one is correct. Additional monitoring, sensor evidence, command validation, or a separate arbitration mechanism is therefore required when continued operation depends on isolating the faulty channel.

Triple-channel architectures provide additional fault-isolation capability because three independently operating channels can support majority voting for suitable functions. If two channels agree and one produces substantially different information, the inconsistent channel can potentially be isolated. Triple redundancy increases hardware, wiring, power, thermal, communication, software, and verification complexity, so its application must be driven by system safety requirements rather than by redundancy alone.

Voting can be applied at different architectural levels. Systems may compare raw sensor measurements, estimated states, flight modes, calculated control commands, or health information. Voting too early can conceal useful diagnostic information, while voting too late can allow an erroneous value to propagate through multiple functions. The selected voting boundary should therefore support rapid fault isolation while preserving independence and avoiding unnecessary coupling among otherwise separate flight-control channels.

Cross-monitoring complements voting by continuously comparing redundant channels. An FCC can evaluate whether another channel\'s attitude, position, angular rate, mode state, timing, or actuator commands remain within defined disagreement limits. Cross-monitoring also identifies frozen data, delayed execution, unexpected resets, and communication failures. Thresholds must account for legitimate numerical differences so that normal computational variation is not incorrectly classified as a fault.

Sensor redundancy is fundamental because multiple computers cannot maintain reliable flight if they all receive the same incorrect aircraft-state information. Multiple IMUs, GNSS receivers, air-data sources, altitude sensors, and other critical measurements can provide independent evidence of vehicle behavior. Sensor-fusion algorithms can reject inconsistent measurements and continue with remaining valid sources, although the resulting navigation accuracy or operational envelope may be reduced.

Sensor diversity can provide protection beyond identical duplication. Two identical sensors may respond similarly to vibration, temperature, electromagnetic interference, software defects, or environmental conditions. Combining different sensing principles or independently located sensors can reduce susceptibility to common-mode failures. Diversity must nevertheless be balanced against calibration complexity, differing error characteristics, additional interfaces, and the verification burden created by heterogeneous equipment.

Power redundancy prevents a single electrical failure from eliminating all flight-control capability. Independent battery feeds, DC/DC converters, protected buses, circuit protection, and power-monitoring functions can supply separate FCC and sensor channels. Essential flight-control resources should avoid unnecessary common electrical dependencies. Cross-tied power may provide useful backup capability, but isolation mechanisms must prevent a short circuit or converter fault from propagating between otherwise independent power domains.

Communication redundancy is equally important in distributed avionics. Separate buses, network paths, or point-to-point interfaces can preserve access to sensors and actuators after a communication failure. Redundant networks should consider not only physical wiring but also switches, gateways, transceivers, synchronization sources, and protocol dependencies. A duplicated cable connected through one common network device may still represent a single point of failure.

Timing resources can also create hidden dependencies. Redundant FCCs may require synchronized time for sensor alignment, voting, event correlation, and distributed control, yet reliance on one clock source can create a common vulnerability. Architectures can provide independent clocks with monitored synchronization or redundant time sources. Loss of precise synchronization should result in a defined degraded condition rather than uncontrolled disagreement among flight-control channels.

Actuator redundancy determines whether valid redundant computation can still influence the aircraft after a mechanical or electronic failure. Critical control functions may use multiple actuators, independent servo channels, distributed propulsion units, or alternative control effectors. Feedback sensors allow the FCC to determine whether commanded movement occurred. When one effector becomes unavailable, control allocation can redistribute required forces and moments if sufficient remaining authority exists.

Distributed propulsion offers additional redundancy opportunities for eVTOL cargo UAVs. Multiple motors and propulsors can allow continued flight after loss of an individual propulsion unit, provided aircraft geometry, available thrust, power capacity, and control laws support the failure condition. Motor count alone does not guarantee tolerance because several propulsion units may share an inverter, battery bus, cooling system, structural support, or communication path that can create a common failure.

Redundancy management determines how available resources are reconfigured after a fault. The system must detect the failure, isolate the affected channel, confirm remaining capability, and establish a stable configuration without introducing excessive control transients. Reconfiguration may involve switching sensor sources, removing an FCC from voting, transferring network paths, redistributing propulsion, limiting maneuverability, or entering a predefined degraded flight mode.

Fail-operational and fail-safe objectives represent different redundancy goals. A fail-operational architecture maintains sufficient functionality to continue controlled operation after a defined failure, whereas a fail-safe architecture prioritizes transition toward a safe condition. Cargo UAV missions may require combinations of both concepts. For example, the aircraft may remain fully controllable after one FCC failure but subsequently divert or land because redundancy has been reduced below the level required for normal mission continuation.

Common-cause failure analysis is essential because nominally redundant components may still fail together. Shared software, requirements errors, environmental exposure, manufacturing defects, cooling systems, power sources, maintenance procedures, or physical damage can defeat multiple channels simultaneously. Physical separation, electrical isolation, independent routing, design diversity, and fault containment help ensure that redundant channels provide genuine independence rather than merely duplicated hardware.

Software redundancy requires particular care. Running identical software on multiple processors protects against random hardware faults but may not protect against a systematic software defect triggered by the same input. Architectural monitoring, independent safety functions, diverse implementations, or dissimilar verification approaches can reduce selected systematic risks. The degree of software diversity should reflect the safety objective and the complexity introduced by maintaining multiple implementations.

Physical installation influences redundancy effectiveness. Redundant FCCs located next to each other may both be affected by fire, fluid ingress, impact, overheating, connector damage, or localized structural failure. Similarly, redundant harnesses routed through the same bundle can be severed together. Separation should therefore be considered across equipment location, wiring routes, connectors, power distribution, cooling, antennas, and sensors according to credible aircraft-level hazards.

Redundancy must be coordinated with flight-mode management. Losing one FCC during cruise may allow continued operation with reduced redundancy, while the same configuration may not be acceptable before takeoff or during a demanding transition mode. The system should know both current capability and the redundancy required for the next flight phase. Entry into a critical mode can be inhibited when insufficient independent resources remain available.

Health monitoring provides the information required for this capability assessment. Each redundant channel can report processor status, memory integrity, timing performance, sensor validity, communication condition, power quality, actuator availability, and internal diagnostic results. The redundancy manager combines this information with cross-channel comparisons to determine which resources remain trustworthy and which operational modes can still be supported safely.

Cargo configuration can affect redundancy requirements because aircraft mass, center of gravity, and inertia influence the amount of control authority required after failures. A heavily loaded aircraft may have less performance margin after losing a propulsion unit than a lightly loaded aircraft. Redundancy management should therefore evaluate actual aircraft configuration when determining whether remaining actuators and propulsion systems can support continued flight, diversion, hover, transition, or landing.

Initialization must verify redundant resources before flight. Merely detecting two or three installed FCCs is insufficient; each required channel must demonstrate valid power, sensors, software configuration, communication, timing, and actuator interfaces. Preflight tests can identify latent faults that would otherwise remain hidden until another failure occurs. Dispatch or arming logic should ensure that the available redundancy satisfies the requirements for the intended mission.

Maintenance and diagnostics are important because redundancy can conceal failures during normal operation. A system may continue functioning correctly after one channel fails, allowing the defect to remain unnoticed unless health information is recorded and reported. Built-in test, fault logging, maintenance messages, and post-flight analysis help ensure that degraded redundancy is restored before subsequent missions and prevent repeated operation with hidden loss of fault tolerance.

Verification of redundant flight control requires deliberate failure injection. Simulation, software-in-the-loop, and hardware-in-the-loop environments can disconnect sensors, corrupt data, reset FCCs, interrupt networks, remove power channels, or simulate failed actuators and propulsion units. Testing must verify detection, voting, isolation, reconfiguration, degraded operation, and recovery while confirming that transient behavior remains within acceptable aircraft limits.

Integrated ground and flight tests then demonstrate redundancy under representative physical conditions. Tests should examine individual failures, latent faults, selected combinations, and failures occurring during critical transitions such as takeoff, hover, conversion, approach, and landing. Verification must also address common dependencies because successfully disconnecting one FCC provides little evidence about the system\'s ability to survive failures that affect several channels simultaneously.

For a scalable cargo UAV family, redundancy architecture becomes increasingly significant as aircraft mass, mission range, autonomy, and consequence of failure increase. A 2.5-ton platform may establish the fundamental redundant control architecture, while 5-ton and future 10-ton platforms may require stronger separation, additional channels, more extensive propulsion tolerance, and higher system assurance. Common architectural principles can remain reusable even when implementation rigor increases.

Ultimately, flight control redundancy creates multiple credible paths for maintaining aircraft control when components fail. Independent sensing establishes trustworthy state information, redundant FCCs preserve computation, separated networks and power domains maintain connectivity, and redundant actuators or propulsion preserve control authority. Cross-monitoring, voting, fault isolation, and reconfiguration integrate these resources into a coherent architecture capable of supporting safe autonomous cargo UAV operation.

비행제어 이중화(Flight Control Redundancy)는 특정 고장이 발생한 이후에도 UAV가 제어 가능한 비행을 유지할 수 있도록 여러 개의 독립적인 센싱, 연산, 통신, 전원 및 구동 자원을 제공하는 아키텍처 원칙이다. 화물 UAV에서 이중화는 단순히 비행제어컴퓨터(Flight Control Computer, FCC)를 복제하는 수준을 넘어야 한다. 목표는 개별 구성요소 또는 전체 제어채널을 사용할 수 없게 되더라도 충분한 제어 권한(Control Authority), 상태정보 및 시스템 무결성을 유지하는 것이다.

비행제어채널(Flight Control Channel)은 일반적으로 센서 입력, 처리 하드웨어, 비행제어 소프트웨어, 통신 인터페이스, 전원공급장치 및 액추에이터나 추진제어기와의 연결을 포함한다. 여러 FCC가 동일한 IMU, 전력변환기, 네트워크 스위치 또는 통신 버스에 의존한다면 해당 공유 자원의 고장으로 모든 채널이 동시에 무력화될 수 있다. 따라서 효과적인 이중화는 단순히 컴퓨터의 개수를 세는 것이 아니라 완전한 기능 경로(Functional Path)를 식별하는 것에서 시작한다.

이중 채널 아키텍처(Dual-Channel Architecture)는 서로를 상호감시(Cross-Monitoring)할 수 있는 두 개의 비행제어 경로를 제공한다. 각 채널은 항공기 상태와 제어명령을 독립적으로 계산하여 채널 간 불일치를 신속하게 검출할 수 있다. 그러나 두 채널의 결과가 서로 다르다는 사실만으로 어느 채널이 올바른지를 판단할 수는 없다. 따라서 지속적인 운용을 위해 고장 채널을 격리해야 하는 경우 추가적인 감시, 센서 근거, 명령 검증 또는 별도의 중재 메커니즘(Arbitration Mechanism)이 필요하다.

삼중 채널 아키텍처(Triple-Channel Architecture)는 독립적으로 동작하는 세 개의 채널을 이용하여 적절한 기능에 대해 다수결 투표(Majority Voting)를 수행할 수 있으므로 추가적인 고장격리 능력을 제공한다. 두 채널이 일치하고 하나의 채널이 크게 다른 정보를 생성한다면 불일치 채널을 고장 채널로 판단하여 격리할 수 있다. 그러나 삼중 이중화는 하드웨어, 배선, 전원, 열관리, 통신, 소프트웨어 및 검증의 복잡성을 증가시키므로 단순히 이중화 수준을 높이기 위한 목적이 아니라 시스템 안전 요구사항에 따라 적용해야 한다.

투표(Voting)는 아키텍처의 서로 다른 계층에서 적용할 수 있다. 시스템은 원시 센서 측정값, 추정 상태, 비행모드, 계산된 제어명령 또는 상태정보를 비교할 수 있다. 너무 이른 단계에서 투표하면 유용한 진단정보가 사라질 수 있고, 너무 늦은 단계에서 투표하면 잘못된 값이 여러 기능으로 전파될 수 있다. 따라서 투표 경계(Voting Boundary)는 독립성을 유지하고 불필요한 채널 간 결합을 방지하면서 신속한 고장격리를 지원하도록 선정해야 한다.

상호감시(Cross-Monitoring)는 중복 채널을 지속적으로 비교하여 투표 기능을 보완한다. FCC는 다른 채널의 자세, 위치, 각속도, 모드 상태, 타이밍 또는 액추에이터 명령이 정의된 불일치 한계 내에 있는지를 평가할 수 있다. 상호감시는 데이터 고착(Frozen Data), 실행 지연, 예상하지 못한 리셋 및 통신 고장도 식별할 수 있다. 정상적인 수치연산 차이가 고장으로 잘못 분류되지 않도록 임계값은 허용 가능한 계산상의 차이를 고려하여 설정해야 한다.

센서 이중화(Sensor Redundancy)는 여러 컴퓨터가 동일하게 잘못된 항공기 상태정보를 수신한다면 신뢰할 수 있는 비행을 유지할 수 없기 때문에 매우 중요하다. 다중 IMU, GNSS 수신기, 대기자료센서, 고도센서 및 기타 중요 측정장치는 항공기 동작에 대한 독립적인 근거를 제공할 수 있다. 센서융합 알고리즘(Sensor-Fusion Algorithm)은 일관되지 않은 측정값을 배제하고 남아 있는 유효한 센서를 사용하여 계속 동작할 수 있지만, 그 결과 항법 정확도 또는 운용영역이 제한될 수 있다.

센서 다양성(Sensor Diversity)은 동일한 센서를 단순히 복제하는 것보다 더 높은 보호능력을 제공할 수 있다. 동일한 두 센서는 진동, 온도, 전자기 간섭, 소프트웨어 결함 또는 환경조건에 유사하게 반응할 수 있다. 서로 다른 센싱 원리를 결합하거나 독립적인 위치에 센서를 설치하면 공통모드고장(Common-Mode Failure)에 대한 취약성을 줄일 수 있다. 그러나 다양성은 보정 복잡성, 서로 다른 오차 특성, 추가 인터페이스 및 이종 장비로 인해 증가하는 검증 부담과 균형을 이루어야 한다.

전원 이중화(Power Redundancy)는 하나의 전기적 고장으로 모든 비행제어 능력이 상실되는 것을 방지한다. 독립적인 배터리 공급경로, DC/DC 컨버터, 보호된 전원버스, 회로보호장치 및 전원감시 기능을 통해 서로 다른 FCC와 센서 채널에 독립적으로 전원을 공급할 수 있다. 필수 비행제어 자원은 불필요한 공통 전기 의존성을 피해야 한다. 교차연결 전원(Cross-Tied Power)은 유용한 백업 기능을 제공할 수 있지만 단락이나 컨버터 고장이 독립적인 전원 도메인 사이로 전파되지 않도록 격리 메커니즘이 필요하다.

통신 이중화(Communication Redundancy)도 분산형 항공전자(Distributed Avionics)에서 동일하게 중요하다. 별도의 버스, 네트워크 경로 또는 점대점 인터페이스(Point-to-Point Interface)를 사용하면 통신 고장 이후에도 센서와 액추에이터에 대한 접근을 유지할 수 있다. 중복 네트워크는 물리적 배선뿐 아니라 스위치, 게이트웨이, 트랜시버, 동기화 소스 및 프로토콜 의존성까지 고려해야 한다. 두 개의 케이블을 사용하더라도 하나의 공통 네트워크 장치에 연결되어 있다면 여전히 단일고장점(Single Point of Failure)이 될 수 있다.

타이밍 자원(Timing Resource) 역시 숨겨진 공통 의존성을 만들 수 있다. 중복 FCC는 센서 정렬, 투표, 이벤트 상관관계 및 분산제어를 위해 동기화된 시간이 필요할 수 있지만 하나의 클록 소스에 의존하면 공통 취약점이 발생한다. 독립적인 클록을 사용하면서 동기화 상태를 감시하거나 중복 시간원을 제공할 수 있다. 정밀한 동기화를 상실한 경우 비행제어 채널 간의 통제되지 않은 불일치가 아니라 사전에 정의된 성능저하 상태(Degraded Condition)로 전환해야 한다.

액추에이터 이중화(Actuator Redundancy)는 기계적 또는 전자적 고장 이후에도 정상적인 중복 연산 결과가 실제 항공기 운동에 영향을 줄 수 있는지를 결정한다. 중요한 제어기능은 다중 액추에이터, 독립적인 서보 채널, 분산추진장치 또는 대체 제어효과기(Control Effector)를 사용할 수 있다. 피드백 센서를 통해 FCC는 명령된 동작이 실제로 수행되었는지를 확인할 수 있다. 하나의 제어효과기를 사용할 수 없게 되면 충분한 제어 권한이 남아 있는 경우 제어할당(Control Allocation)을 통해 필요한 힘과 모멘트를 다른 제어효과기로 재분배할 수 있다.

분산추진(Distributed Propulsion)은 eVTOL 화물 UAV에서 추가적인 이중화 가능성을 제공한다. 여러 모터와 추진장치를 사용하면 항공기 형상, 사용 가능한 추력, 전력용량 및 제어법칙이 고장상태를 지원하는 경우 하나의 추진장치를 상실한 이후에도 비행을 계속할 수 있다. 그러나 여러 추진장치가 하나의 인버터, 배터리 버스, 냉각시스템, 구조적 지지부 또는 통신 경로를 공유할 수 있으므로 단순히 모터의 개수가 많다고 해서 내고장성이 보장되는 것은 아니다.

이중화 관리(Redundancy Management)는 고장 이후 사용 가능한 자원을 어떻게 재구성할 것인지를 결정한다. 시스템은 고장을 검출하고 영향을 받은 채널을 격리하며 남아 있는 능력을 확인한 후 과도한 제어 과도현상(Control Transient)을 발생시키지 않고 안정적인 구성을 확립해야 한다. 재구성에는 센서 소스 전환, 특정 FCC의 투표 제외, 네트워크 경로 전환, 추진력 재분배, 기동성 제한 또는 사전에 정의된 성능저하 비행모드로의 전환 등이 포함될 수 있다.

고장 후 운용유지(Fail-Operational)와 고장안전(Fail-Safe)은 서로 다른 이중화 목표를 나타낸다. 고장 후 운용유지 아키텍처는 정의된 고장이 발생한 이후에도 제어 가능한 운용을 계속할 수 있는 충분한 기능을 유지하는 반면, 고장안전 아키텍처는 안전한 상태로 전환하는 것을 우선한다. 화물 UAV 임무에서는 두 개념을 조합할 수 있다. 예를 들어 하나의 FCC 고장 후에도 항공기는 완전한 제어 능력을 유지할 수 있지만, 이중화 수준이 정상 임무 지속에 필요한 수준 이하로 감소했다면 이후 우회하거나 착륙할 수 있다.

공통원인고장 분석(Common-Cause Failure Analysis)은 명목상 독립적인 중복 구성요소가 동시에 고장날 수 있기 때문에 필수적이다. 공유 소프트웨어, 요구사항 오류, 환경 노출, 제조 결함, 냉각시스템, 전원, 정비절차 또는 물리적 손상은 여러 채널을 동시에 무력화할 수 있다. 물리적 분리, 전기적 격리, 독립적인 배선 경로, 설계 다양성(Design Diversity) 및 고장격리(Fault Containment)는 중복 채널이 단순히 하드웨어를 복제하는 것이 아니라 실제 독립성을 제공하도록 한다.

소프트웨어 이중화(Software Redundancy)는 특히 신중하게 설계해야 한다. 여러 프로세서에서 동일한 소프트웨어를 실행하면 무작위 하드웨어 고장(Random Hardware Fault)에 대해서는 보호할 수 있지만 동일한 입력에 의해 발생하는 체계적 소프트웨어 결함(Systematic Software Fault)에는 효과적이지 않을 수 있다. 아키텍처 감시, 독립적인 안전기능, 다양한 구현 또는 상이한 검증방법을 통해 특정 체계적 위험을 줄일 수 있다. 소프트웨어 다양성의 수준은 안전목표와 다중 구현을 유지하면서 발생하는 복잡성을 함께 고려하여 결정해야 한다.

물리적 설치(Physical Installation)는 이중화의 실질적인 효과에 영향을 준다. 서로 인접하게 설치된 중복 FCC는 화재, 액체 유입, 충격, 과열, 커넥터 손상 또는 국부적인 구조 파손의 영향을 동시에 받을 수 있다. 마찬가지로 동일한 하니스 번들(Harness Bundle)을 따라 배선된 중복 회로는 동시에 절단될 수 있다. 따라서 신뢰할 수 있는 항공기 수준 위험요인을 기준으로 장비 위치, 배선 경로, 커넥터, 전력분배, 냉각, 안테나 및 센서에 걸쳐 물리적 분리를 고려해야 한다.

이중화는 비행모드관리(Flight-Mode Management)와 연계되어야 한다. 순항 중 하나의 FCC를 상실하더라도 이중화 수준을 낮춘 상태에서 비행을 계속할 수 있지만, 동일한 시스템 상태가 이륙 전이나 복잡한 전환비행(Transition Mode)에 진입하기에는 허용되지 않을 수 있다. 시스템은 현재 사용 가능한 능력뿐 아니라 다음 비행 단계에서 요구되는 이중화 수준도 파악해야 한다. 충분한 독립 자원이 남아 있지 않다면 중요한 비행모드로의 진입을 차단할 수 있다.

상태감시(Health Monitoring)는 이러한 시스템 능력 평가에 필요한 정보를 제공한다. 각 중복 채널은 프로세서 상태, 메모리 무결성, 타이밍 성능, 센서 유효성, 통신 상태, 전원 품질, 액추에이터 가용성 및 내부 진단결과를 보고할 수 있다. 이중화 관리자(Redundancy Manager)는 이러한 정보와 채널 간 비교 결과를 결합하여 어떤 자원을 계속 신뢰할 수 있는지, 그리고 어떤 운용모드를 안전하게 지원할 수 있는지를 결정한다.

화물 구성(Cargo Configuration)은 항공기의 질량, 무게중심(Center of Gravity, CG) 및 관성이 고장 이후 필요한 제어 권한에 영향을 미치기 때문에 이중화 요구사항에도 영향을 줄 수 있다. 중량이 큰 항공기는 가벼운 항공기보다 하나의 추진장치를 상실한 이후 성능 여유가 작을 수 있다. 따라서 이중화 관리 기능은 남아 있는 액추에이터와 추진시스템이 비행 지속, 우회, 호버링, 전환비행 또는 착륙을 지원할 수 있는지를 판단할 때 실제 항공기 구성을 평가해야 한다.

초기화(Initialization) 단계에서는 비행 전에 중복 자원을 검증해야 한다. 단순히 두 개 또는 세 개의 FCC가 설치되어 있음을 확인하는 것으로는 충분하지 않으며, 필요한 각 채널이 정상적인 전원, 센서, 소프트웨어 구성, 통신, 타이밍 및 액추에이터 인터페이스를 갖추고 있음을 입증해야 한다. 비행 전 시험(Preflight Test)은 다른 고장이 발생할 때까지 발견되지 않을 수 있는 잠재고장(Latent Fault)을 식별할 수 있다. 출동 또는 무장 로직(Dispatch or Arming Logic)은 사용 가능한 이중화가 계획된 임무 요구사항을 만족하는지 확인해야 한다.

정비 및 진단(Maintenance and Diagnostics)은 이중화로 인해 정상 운용 중 고장이 숨겨질 수 있기 때문에 중요하다. 하나의 채널이 고장난 이후에도 시스템이 정상적으로 기능할 수 있으므로 상태정보를 기록하고 보고하지 않으면 해당 결함이 발견되지 않을 수 있다. 내장시험(Built-In Test), 고장기록, 정비 메시지 및 비행 후 분석(Post-Flight Analysis)은 다음 임무 전에 저하된 이중화 상태를 복구하도록 하며, 내고장성이 숨겨진 상태로 감소한 채 반복 운용되는 것을 방지한다.

중복 비행제어의 검증(Verification)은 의도적인 고장주입(Failure Injection)을 필요로 한다. 시뮬레이션, 소프트웨어 인더 루프(Software-in-the-Loop, SIL) 및 하드웨어 인더 루프(Hardware-in-the-Loop, HIL) 환경에서 센서를 분리하고, 데이터를 손상시키고, FCC를 리셋하고, 네트워크를 차단하며, 전원 채널을 제거하거나 액추에이터 및 추진장치 고장을 모사할 수 있다. 시험에서는 고장검출, 투표, 격리, 재구성, 성능저하 운용 및 복구를 검증하는 동시에 과도상태가 허용 가능한 항공기 한계 내에 유지되는지 확인해야 한다.

통합 지상시험(Integrated Ground Test)과 비행시험(Flight Test)은 대표적인 물리적 조건에서 이중화 기능을 검증한다. 시험에서는 개별 고장, 잠재고장, 선택된 복합고장 및 이륙, 호버링, 전환, 접근, 착륙과 같은 중요한 비행단계에서 발생하는 고장을 평가해야 한다. 또한 하나의 FCC를 성공적으로 차단하는 시험만으로는 여러 채널에 동시에 영향을 주는 고장에 대한 생존 능력을 충분히 입증할 수 없으므로 공통 의존성(Common Dependency)에 대한 검증도 필요하다.

확장 가능한 화물 UAV 제품군(Scalable Cargo UAV Family)에서는 항공기 질량, 임무거리, 자율성 및 고장 결과의 심각성이 증가할수록 이중화 아키텍처의 중요성이 더욱 커진다. 2.5톤급 플랫폼에서 기본적인 중복 제어 아키텍처를 확립하고, 5톤 및 향후 10톤급 플랫폼에서는 더욱 강력한 물리적 분리, 추가 채널, 향상된 추진 고장 허용능력 및 높은 수준의 시스템 보증(System Assurance)이 요구될 수 있다. 구현의 엄격성이 증가하더라도 공통적인 아키텍처 원칙은 제품군 전체에서 재사용할 수 있다.

궁극적으로 비행제어 이중화(Flight Control Redundancy)는 구성요소가 고장나더라도 항공기 제어를 유지할 수 있는 여러 개의 신뢰 가능한 경로를 구축한다. 독립적인 센싱은 신뢰할 수 있는 상태정보를 확보하고, 중복 FCC는 연산 기능을 유지하며, 분리된 네트워크와 전원 도메인은 연결성을 보존하고, 중복 액추에이터 또는 추진시스템은 제어 권한을 유지한다. 상호감시, 투표, 고장격리 및 재구성 기능은 이러한 자원을 하나의 일관된 아키텍처로 통합하여 안전한 자율 화물 UAV 운용을 지원한다.
