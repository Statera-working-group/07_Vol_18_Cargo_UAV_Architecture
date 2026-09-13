**Volume 18. Cargo UAV Architecture**


# Chapter 02. Avionics Architecture

##  

## 02.01. FCC/FMC Architecture

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

The Flight Control Computer (FCC) and Flight Management Computer (FMC) form two complementary computational domains within a cargo UAV avionics architecture. The FCC is responsible for real-time stabilization and control of the aircraft, while the FMC manages higher-level mission, navigation, trajectory, and operational objectives. Separating these domains allows deterministic flight-control functions to remain protected from computationally complex mission-management workloads.

The FCC operates at the innermost layer of the flight-control architecture. It continuously receives measurements from inertial measurement units, air-data sensors, GNSS receivers, attitude and heading systems, propulsion controllers, and other flight-critical sources. These inputs are processed through estimation and control algorithms that generate actuator commands for aerodynamic surfaces, motors, propellers, rotors, or thrust-vectoring mechanisms.

Real-time determinism is a fundamental FCC requirement because aircraft stability depends on predictable sensing, computation, and actuation latency. Attitude, angular-rate, altitude, velocity, and position control loops may operate at different update frequencies, but each must remain within defined timing limits. The FCC therefore emphasizes deterministic scheduling, bounded execution time, low communication latency, and controlled software partitioning rather than maximum computational throughput.

The FMC operates above these fast control loops and determines where and how the aircraft should fly. It manages flight plans, waypoints, route constraints, altitude profiles, speed targets, mission phases, energy considerations, and destination requirements. In an autonomous cargo UAV, the FMC can additionally coordinate departure, cruise, approach, landing, diversion, contingency routing, and interfaces with ground-based mission-planning or traffic-management systems.

A useful architectural distinction is that the FMC produces intent while the FCC converts that intent into physically achievable aircraft motion. The FMC may command a desired trajectory, altitude, airspeed, heading, or flight mode, but the FCC determines the required control response using current aircraft states. This hierarchy prevents mission software from directly manipulating actuators and establishes a controlled boundary between strategic navigation decisions and safety-critical vehicle dynamics.

Navigation functions bridge the two computational domains. GNSS, inertial navigation, air-data measurements, terrain information, and other navigation sources can be fused to estimate the aircraft state. Depending on system partitioning, high-rate state estimation may reside within the FCC, while route-level navigation and trajectory generation reside within the FMC. Clearly defined interfaces prevent conflicting estimates or duplicated control authority from propagating through the avionics system.

For a large autonomous cargo UAV, the FCC architecture should not be considered a single general-purpose computer. Flight-critical implementations commonly require redundant computational channels, independent sensor paths, fault detection, cross-channel monitoring, and controlled failover behavior. Multiple FCC channels can independently calculate flight states and commands, allowing disagreement detection and continued operation when an individual processor, sensor interface, communication path, or power domain fails.

The FMC can also employ redundancy, although its failure characteristics differ from those of the FCC. Temporary loss of mission optimization should not immediately destabilize the aircraft because the FCC must retain sufficient local authority to maintain safe flight. A degraded FMC condition can therefore trigger predefined behaviors such as holding a stable trajectory, continuing toward a validated waypoint, entering a loiter pattern, returning to base, diverting, or executing another certified contingency strategy.

Communication between FCC and FMC requires explicit data ownership and command authority. Typical information flowing toward the FCC includes trajectory references, navigation targets, requested flight modes, speed commands, and mission-phase transitions. Information returning toward the FMC includes aircraft state, control mode, navigation quality, system health, propulsion status, energy availability, fault conditions, and whether requested trajectories remain feasible under current vehicle limitations.

The avionics network surrounding these computers must support both deterministic flight-critical communication and higher-bandwidth mission data. The broader cargo UAV structure explicitly includes aerospace protocols such as ARINC 429, ARINC 664/AFDX, MIL-STD-1553, and Time-Triggered Ethernet as separate architectural topics. Their placement indicates that protocol selection should be treated as part of the overall avionics partitioning rather than as an isolated communication decision.

Power architecture is equally important because computational redundancy provides little benefit when redundant computers share a common electrical failure point. FCC and FMC channels should therefore be considered together with independent power feeds, protected distribution, monitoring, reset strategies, and backup energy sources. Critical sensor and communication paths must also be partitioned so that a single power-distribution, connector, harness, or network fault does not disable every control channel simultaneously.

The boundary between flight control and propulsion becomes especially important in cargo UAVs using distributed electric propulsion, hybrid-electric propulsion, or eVTOL configurations. The FCC may command thrust allocation rather than a single engine throttle, while lower-level propulsion controllers regulate individual motors, inverters, generators, or rotor systems. Control allocation must account for actuator limits, failures, asymmetric thrust, vehicle configuration, and transitions between different aerodynamic operating regimes.

The FMC must simultaneously consider mission feasibility at a much longer time horizon. For electric and hybrid cargo aircraft, route planning cannot be separated from energy management. Remaining battery energy, fuel state, predicted winds, payload mass, reserve requirements, alternate landing sites, propulsion degradation, and environmental constraints can influence trajectory decisions. The FMC can therefore become a central coordinator between navigation, mission planning, energy management, and contingency management.

Cargo operations introduce additional state information that conventional small UAV autopilots may not require. Payload mass, center-of-gravity condition, cargo-lock status, and cargo-system health can influence allowable flight envelopes and mission authorization. The volume structure consequently places cargo weight sensing, CG monitoring, cargo locking, environmental monitoring, and payload interfaces in a dedicated Cargo Management System, which should exchange validated operational states with the FCC/FMC architecture.

Ground systems represent another important architectural boundary. The Ground Control Station can provide mission plans, operator commands, route modifications, health monitoring, and contingency instructions, but safe aircraft operation should not depend on uninterrupted ground communication. The onboard FCC/FMC architecture must maintain sufficient autonomous capability to continue controlled flight when the datalink is delayed, degraded, interrupted, or unavailable for a defined period.

Integration with unmanned traffic management further expands the FMC role. Geofencing constraints, airspace restrictions, traffic information, collision-avoidance requirements, and approved routes can modify mission-level trajectory planning. These external constraints should enter through controlled interfaces rather than directly influencing actuator commands. The FCC remains responsible for executing validated trajectories while respecting aircraft dynamics, control limits, and immediate flight-safety requirements.

Fault management therefore spans multiple hierarchical layers. Hardware monitoring detects processor, memory, power, communication, sensor, and actuator faults; the FCC determines whether stable control can continue; and the FMC evaluates whether the original mission remains achievable. A propulsion fault, for example, may first require immediate control reconfiguration by the FCC and subsequently require route replanning, diversion, or emergency landing selection by the FMC.

As cargo UAV size increases from the 2.5-ton class toward 5-ton and 10-ton architectures represented in the volume structure, avionics partitioning becomes increasingly important. Higher payload, longer range, hybrid propulsion, more complex energy systems, and expanded operational environments increase the number of interacting subsystems. The FCC/FMC architecture therefore becomes a hierarchical safety backbone connecting vehicle dynamics, navigation, propulsion, mission management, cargo systems, ground control, and external airspace services.

비행 제어 컴퓨터(Flight Control Computer, FCC)와 비행 관리 컴퓨터(Flight Management Computer, FMC)는 화물 무인항공기(Cargo UAV)의 항공전자 아키텍처(Avionics Architecture)에서 서로 보완적인 두 개의 연산 영역(Computational Domain)을 구성한다. FCC는 항공기의 실시간 안정화(Real-time Stabilization)와 제어(Control)를 담당하고, FMC는 상위 수준의 임무(Mission), 항법(Navigation), 궤적(Trajectory), 운용 목표(Operational Objective)를 관리한다. 이러한 영역 분리는 결정론적 비행 제어 기능(Deterministic Flight-Control Function)을 복잡한 임무 관리 연산 부하로부터 보호할 수 있게 한다.

FCC는 비행 제어 아키텍처(Flight-Control Architecture)의 가장 내부 계층(Innermost Layer)에서 동작한다. FCC는 관성 측정 장치(Inertial Measurement Unit, IMU), 대기자료 센서(Air-Data Sensor), 위성항법시스템 수신기(GNSS Receiver), 자세 및 방위 시스템(Attitude and Heading System), 추진 제어기(Propulsion Controller), 기타 비행 필수 센서로부터 측정값을 지속적으로 수신한다. 이러한 입력은 상태 추정(State Estimation) 및 제어 알고리즘(Control Algorithm)을 통해 처리되어 조종면, 모터, 프로펠러, 로터 또는 추력 벡터링 장치(Thrust-Vectoring Mechanism)를 위한 액추에이터 명령(Actuator Command)으로 변환된다.

실시간 결정성(Real-Time Determinism)은 항공기 안정성이 예측 가능한 센싱(Sensing), 연산(Computation), 구동(Actuation) 지연시간에 의존하기 때문에 FCC의 핵심 요구사항이다. 자세(Attitude), 각속도(Angular Rate), 고도(Altitude), 속도(Velocity), 위치(Position) 제어 루프는 서로 다른 갱신 주기로 동작할 수 있지만 각각 정의된 시간 한계 내에서 실행되어야 한다. 따라서 FCC는 최대 연산 처리량보다는 결정론적 스케줄링(Deterministic Scheduling), 제한된 실행시간(Bounded Execution Time), 낮은 통신 지연(Low Communication Latency), 통제된 소프트웨어 파티셔닝(Software Partitioning)을 중요하게 다룬다.

FMC는 이러한 고속 제어 루프(Fast Control Loop)의 상위에서 동작하며 항공기가 어디로, 어떻게 비행해야 하는지를 결정한다. FMC는 비행 계획(Flight Plan), 웨이포인트(Waypoint), 경로 제약(Route Constraint), 고도 프로파일(Altitude Profile), 속도 목표(Speed Target), 임무 단계(Mission Phase), 에너지 조건(Energy Consideration), 목적지 요구사항(Destination Requirement)을 관리한다. 자율 화물 무인항공기(Autonomous Cargo UAV)에서는 출발, 순항, 접근, 착륙, 우회, 비상 경로 설정과 지상 임무 계획 또는 교통 관리 시스템과의 인터페이스도 조정할 수 있다.

유용한 아키텍처적 구분은 FMC가 비행 의도(Intent)를 생성하고 FCC가 그 의도를 물리적으로 구현 가능한 항공기 운동으로 변환한다는 것이다. FMC는 목표 궤적(Desired Trajectory), 고도, 대기속도(Airspeed), 기수 방향(Heading), 비행 모드(Flight Mode)를 명령할 수 있지만, FCC는 현재 항공기 상태를 기반으로 필요한 제어 응답(Control Response)을 결정한다. 이러한 계층 구조는 임무 소프트웨어가 액추에이터를 직접 조작하는 것을 방지하고 전략적 항법 결정과 안전 필수 비행 동역학(Safety-Critical Flight Dynamics) 사이에 통제된 경계를 형성한다.

항법 기능(Navigation Function)은 두 연산 영역을 연결한다. 위성항법시스템(GNSS), 관성항법(Inertial Navigation), 대기자료 측정(Air-Data Measurement), 지형 정보(Terrain Information), 기타 항법 정보원을 융합하여 항공기 상태를 추정할 수 있다. 시스템 파티셔닝(System Partitioning)에 따라 고주기 상태 추정(High-Rate State Estimation)은 FCC에 배치하고, 경로 수준 항법(Route-Level Navigation)과 궤적 생성(Trajectory Generation)은 FMC에 배치할 수 있다. 명확하게 정의된 인터페이스는 서로 충돌하는 상태 추정이나 중복된 제어 권한이 항공전자 시스템 전체로 전파되는 것을 방지한다.

대형 자율 화물 무인항공기에서 FCC 아키텍처를 하나의 범용 컴퓨터(General-Purpose Computer)로 간주해서는 안 된다. 비행 필수 시스템은 일반적으로 중복 연산 채널(Redundant Computational Channel), 독립 센서 경로(Independent Sensor Path), 고장 감지(Fault Detection), 채널 간 감시(Cross-Channel Monitoring), 통제된 장애 전환(Failover)을 요구한다. 복수의 FCC 채널이 항공기 상태와 제어 명령을 독립적으로 계산함으로써 특정 프로세서, 센서 인터페이스, 통신 경로 또는 전원 영역에서 장애가 발생해도 불일치를 감지하고 운항을 지속할 수 있다.

FMC 역시 중복성(Redundancy)을 적용할 수 있지만 고장 특성은 FCC와 다르다. 임무 최적화(Mission Optimization)가 일시적으로 중단되더라도 FCC가 안전한 비행을 유지할 수 있는 충분한 로컬 제어 권한(Local Control Authority)을 보유한다면 항공기가 즉시 불안정해져서는 안 된다. 따라서 FMC 기능 저하 시 안정된 궤적 유지, 검증된 웨이포인트까지 비행 지속, 선회 대기(Loiter), 기지 복귀(Return to Base), 대체 목적지로 우회(Diversion), 기타 인증된 비상 대응 전략(Contingency Strategy)을 수행하도록 설계할 수 있다.

FCC와 FMC 사이의 통신에는 명확한 데이터 소유권(Data Ownership)과 명령 권한(Command Authority)이 필요하다. FCC 방향으로 전달되는 대표적인 정보에는 궤적 기준값(Trajectory Reference), 항법 목표(Navigation Target), 요청 비행 모드(Requested Flight Mode), 속도 명령(Speed Command), 임무 단계 전환(Mission-Phase Transition)이 포함된다. FMC 방향으로 반환되는 정보에는 항공기 상태, 제어 모드, 항법 품질, 시스템 건전성(System Health), 추진 시스템 상태, 가용 에너지, 고장 상태, 현재 차량 한계에서 요청된 궤적의 실현 가능성 등이 포함된다.

이러한 컴퓨터를 연결하는 항공전자 네트워크(Avionics Network)는 결정론적 비행 필수 통신과 고대역폭 임무 데이터(High-Bandwidth Mission Data)를 모두 지원해야 한다. 화물 무인항공기 전체 구조에는 ARINC 429, ARINC 664/AFDX, MIL-STD-1553, 시간 결정형 이더넷(Time-Triggered Ethernet)과 같은 항공우주 통신 프로토콜(Aerospace Protocol)이 별도의 아키텍처 주제로 구성된다. 이는 프로토콜 선택(Protocol Selection)을 독립적인 통신 문제보다는 전체 항공전자 파티셔닝의 일부로 다루어야 함을 의미한다.

전원 아키텍처(Power Architecture) 역시 중요하다. 중복 컴퓨터가 동일한 공통 전기 고장점(Common Electrical Failure Point)을 공유한다면 연산 중복성의 효과는 크게 감소한다. 따라서 FCC와 FMC 채널은 독립 전원 공급(Independent Power Feed), 보호 전력 분배(Protected Power Distribution), 상태 감시, 리셋 전략(Reset Strategy), 백업 에너지원(Backup Energy Source)과 함께 설계되어야 한다. 핵심 센서와 통신 경로 역시 하나의 전력 분배, 커넥터, 와이어 하니스 또는 네트워크 고장으로 모든 제어 채널이 동시에 정지하지 않도록 분리해야 한다.

비행 제어와 추진 시스템(Propulsion System)의 경계는 분산 전기 추진(Distributed Electric Propulsion), 하이브리드 전기 추진(Hybrid-Electric Propulsion), 전기 수직이착륙(eVTOL) 구성을 사용하는 화물 무인항공기에서 특히 중요하다. FCC는 하나의 엔진 스로틀 대신 추력 분배(Thrust Allocation)를 명령할 수 있으며, 하위 추진 제어기가 개별 모터, 인버터, 발전기 또는 로터 시스템을 제어한다. 제어 할당(Control Allocation)은 액추에이터 한계, 고장, 비대칭 추력(Asymmetric Thrust), 기체 구성, 서로 다른 공력 운용 영역 사이의 천이(Transition)를 고려해야 한다.

동시에 FMC는 훨씬 긴 시간 범위에서 임무 실현 가능성(Mission Feasibility)을 고려해야 한다. 전기식 및 하이브리드 화물 항공기에서는 경로 계획(Route Planning)을 에너지 관리(Energy Management)와 분리하기 어렵다. 잔여 배터리 에너지, 연료 상태, 예상 풍향과 풍속, 탑재화물 질량, 예비 에너지 요구량, 대체 착륙지, 추진 시스템 성능 저하, 환경 제약이 궤적 결정에 영향을 줄 수 있다. 따라서 FMC는 항법, 임무 계획, 에너지 관리, 비상 상황 관리(Contingency Management)를 연결하는 중앙 조정기로 발전할 수 있다.

화물 운송은 일반적인 소형 UAV 자동조종장치(Autopilot)가 요구하지 않는 추가적인 상태 정보를 필요로 한다. 탑재화물 질량(Payload Mass), 무게중심 상태(Center-of-Gravity Condition), 화물 잠금 상태(Cargo-Lock Status), 화물 시스템 건전성(Cargo-System Health)은 허용 가능한 비행 영역(Flight Envelope)과 임무 승인에 영향을 줄 수 있다. 따라서 화물 중량 감지, 무게중심 감시(CG Monitoring), 화물 잠금, 환경 감시, 탑재체 인터페이스(Payload Interface)를 담당하는 전용 화물 관리 시스템(Cargo Management System)은 검증된 운용 상태 정보를 FCC/FMC 아키텍처와 교환해야 한다.

지상 시스템(Ground System)은 또 하나의 중요한 아키텍처 경계를 형성한다. 지상통제소(Ground Control Station, GCS)는 임무 계획, 운용자 명령, 경로 변경, 건전성 감시, 비상 명령을 제공할 수 있지만 안전한 항공기 운용이 지상 통신의 지속적인 연결에 의존해서는 안 된다. 데이터링크(Datalink)가 지연되거나 성능이 저하되거나 일정 기간 단절되더라도 탑재된 FCC/FMC 아키텍처는 제어된 비행을 지속할 수 있는 충분한 자율 기능(Autonomous Capability)을 유지해야 한다.

무인 교통 관리(Unmanned Traffic Management, UTM)와의 통합은 FMC의 역할을 더욱 확장한다. 지오펜싱(Geofencing) 제약, 공역 제한(Airspace Restriction), 교통 정보, 충돌 회피(Collision Avoidance) 요구사항, 승인된 비행 경로가 임무 수준 궤적 계획을 변경할 수 있다. 이러한 외부 제약은 액추에이터 명령에 직접 영향을 주기보다는 통제된 인터페이스를 통해 입력되어야 한다. FCC는 항공기 동역학, 제어 한계, 즉각적인 비행 안전 요구사항을 준수하면서 검증된 궤적을 실행하는 역할을 유지한다.

따라서 고장 관리(Fault Management)는 여러 계층에 걸쳐 수행된다. 하드웨어 감시는 프로세서, 메모리, 전원, 통신, 센서, 액추에이터 고장을 탐지하고, FCC는 안정적인 제어를 계속할 수 있는지를 판단하며, FMC는 기존 임무를 계속 수행할 수 있는지를 평가한다. 예를 들어 추진 시스템 고장은 먼저 FCC에 의한 즉각적인 제어 재구성(Control Reconfiguration)을 요구할 수 있으며, 이후 FMC가 경로 재계획(Route Replanning), 우회 또는 비상 착륙지 선택을 수행할 수 있다.

본 권의 구조에서 제시하는 2.5톤급에서 5톤급, 10톤급 화물 무인항공기 아키텍처로 기체 규모가 증가할수록 항공전자 파티셔닝(Avionics Partitioning)의 중요성도 증가한다. 더 큰 탑재량, 장거리 비행, 하이브리드 추진, 복잡한 에너지 시스템, 확대된 운용 환경은 상호작용하는 서브시스템의 수를 증가시킨다. 따라서 FCC/FMC 아키텍처는 비행 동역학, 항법, 추진, 임무 관리, 화물 시스템, 지상 통제, 외부 공역 서비스를 연결하는 계층형 안전 백본(Hierarchical Safety Backbone)으로 발전한다.

##  

## 02.02. Redundant Avionics Design

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

Redundant avionics design ensures that a cargo UAV can maintain controlled flight when individual computers, sensors, communication links, power sources, or actuators fail. Unlike simple component duplication, effective redundancy requires independent channels, fault containment, continuous health monitoring, and deterministic reconfiguration. The objective is not merely to prevent equipment loss, but to prevent a single failure from becoming a vehicle-level loss of control.

The architecture begins by identifying flight-critical functions and determining how many independent paths are required to preserve them. Flight control, navigation, propulsion control, electrical power, communication, and essential sensing may require different redundancy strategies according to their failure consequences. A cargo UAV carrying substantial payloads generally demands stronger fault tolerance than a small unmanned aircraft because the potential consequences of uncontrolled flight are significantly greater.

Dual redundancy provides two channels performing equivalent functions, allowing one channel to continue operation when the other clearly fails. However, two channels alone cannot always determine which result is correct when their outputs disagree. For this reason, highly critical functions may use triple modular redundancy, where three independent channels calculate comparable results and voting logic identifies an inconsistent channel while the remaining two establish the accepted result.

Triple redundant Flight Control Computers can independently process sensor information, estimate aircraft states, execute control laws, and generate actuator commands. Cross-channel monitoring continuously compares their operating states and calculated outputs. When one FCC produces values outside predefined agreement limits, the architecture can isolate the suspected channel and continue operation using the healthy channels, while recording the fault and notifying higher-level system management.

Redundancy must also extend to sensors because several computers using one common sensor do not create a truly redundant control system. Multiple IMUs, GNSS receivers, air-data sensors, altitude sources, or attitude references can provide independent measurements. Sensor voting, consistency checking, analytical redundancy, and model-based estimation allow the avionics system to detect measurements that diverge from expected aircraft behavior and remove unreliable sources from the active solution.

Navigation redundancy is particularly important for autonomous cargo operations. GNSS may provide highly accurate absolute positioning but can be degraded by interference, blockage, jamming, spoofing, or antenna faults. Inertial navigation can maintain short-term state estimation without external signals, while additional navigation sources can constrain accumulated drift. The avionics architecture should therefore treat navigation as a multi-source estimation problem rather than depending on one positioning technology.

Communication paths between redundant computers must avoid introducing common points of failure. Independent buses, switches, network interfaces, connectors, and harness routes may be required for critical data. Aerospace communication technologies such as ARINC 429, ARINC 664/AFDX, MIL-STD-1553, or Time-Triggered Ethernet can support different redundancy models, but protocol redundancy is effective only when the physical and logical network architecture also provides appropriate fault isolation.

Electrical redundancy is inseparable from computational redundancy. Two FCCs connected to the same unprotected power rail can both disappear after one electrical fault. Critical avionics channels should therefore be distributed across independent or appropriately isolated power domains, with separate protection, conversion, monitoring, and backup capability. Battery-backed essential buses or alternative energy sources can preserve minimum flight-control capability after degradation of the primary electrical system.

Physical separation further reduces common-cause failures. Redundant computers installed together may simultaneously experience fire, water intrusion, impact damage, overheating, electromagnetic interference, or connector failure. Sensor wiring and network harnesses routed through the same vulnerable location can suffer the same problem. Redundant avionics design consequently considers equipment placement, harness routing, thermal zones, grounding, shielding, connector independence, and structural separation as part of system safety.

Fault detection, isolation, and recovery form the operational core of the redundant architecture. Fault detection determines that abnormal behavior exists, fault isolation identifies the affected component or channel, and recovery establishes an appropriate configuration using remaining resources. These functions must operate quickly enough that the aircraft remains within its controllable flight envelope while reconfiguration occurs, particularly during takeoff, landing, transition, or other dynamically sensitive phases.

Redundancy management should distinguish between transient faults and persistent failures. A temporary communication timeout or sensor anomaly does not necessarily justify permanent channel removal, while repeated or physically implausible behavior may require isolation. Health-monitoring logic can therefore use timing thresholds, plausibility checks, disagreement counters, built-in tests, watchdogs, communication supervision, and confidence metrics to determine whether a component should remain active, restart, enter standby, or be disconnected.

Actuator redundancy introduces another level of complexity because computational commands ultimately depend on physical control authority. Conventional aircraft may use redundant servos or control surfaces, while distributed-propulsion UAVs can exploit multiple motors or rotors. If one actuator or propulsion unit fails, control-allocation algorithms can redistribute commands among remaining devices, provided sufficient thrust and control authority remain to maintain a safe flight condition.

A distributed propulsion architecture can therefore provide functional redundancy without requiring every propulsion unit to have an identical standby replacement. The important requirement is vehicle-level controllability after a defined failure. The FCC must understand actuator availability, performance limits, saturation, asymmetric thrust, and degraded dynamics so that commands are allocated only to healthy resources and the aircraft remains inside a reduced but safe operating envelope.

Redundant Flight Management Computers address a different time scale. FMC failure should not interrupt the high-rate stabilization performed by the FCC. A standby or parallel FMC can preserve flight plans, navigation targets, mission states, energy information, and contingency data. If the active FMC fails, another channel can assume mission-management authority while the FCC continues executing the most recently validated flight mode or trajectory during the transition.

Cargo systems must also participate in redundancy management where their state affects flight safety. Payload mass, center of gravity, cargo restraint, door or locking status, and other cargo conditions can modify aircraft limitations. Independent sensing or plausibility checking may therefore be required for safety-relevant cargo information. An invalid cargo measurement should be detected before it causes inappropriate trajectory, performance, energy, or control-envelope calculations.

Ground communication can provide valuable supervision but should not serve as the final redundancy mechanism for onboard flight control. Loss of the Ground Control Station or datalink must not remove the aircraft\'s ability to stabilize itself. Autonomous contingency logic should define responses to communication loss, including continued flight, loiter, return, diversion, or landing according to mission phase, aircraft condition, available energy, weather constraints, and predefined operational rules.

Redundancy also requires protection against common-mode and common-cause failures. Installing three identical computers does not guarantee independence if all contain the same systematic design defect, receive corrupted common data, share one clock, depend on one power converter, or execute identical erroneous software assumptions. Architectural diversity, independent monitoring, partitioning, development assurance, and carefully controlled interfaces can reduce the probability that one cause defeats multiple redundant channels simultaneously.

Graceful degradation is a central design principle. A redundant cargo UAV should not be viewed only as either fully operational or failed. Loss of one component may reduce mission capability while preserving safe flight. The system can progressively restrict speed, maneuvering, altitude, route options, autonomous functions, or payload operations as redundancy is consumed, eventually transitioning to diversion or emergency landing when the remaining safety margin becomes insufficient.

Built-in test and maintenance functions complete the redundancy lifecycle. Power-on tests, continuous monitoring, maintenance diagnostics, fault histories, event logs, and channel-performance records help identify latent failures before another failure occurs. This is particularly important because an unnoticed standby-channel failure can silently eliminate redundancy. Maintenance systems should therefore verify not only active equipment but also components that may be required only during abnormal operation.

The overall Volume 18 structure places redundant avionics alongside FCC/FMC architecture, DO-254 hardware design, avionics power architecture, cooling, flight-control redundancy, failsafe design, Ground Control Station redundancy, and UAV safety architecture. This organization reflects an important principle: redundancy is not a single avionics feature but a system-level property spanning computation, sensing, networks, power, propulsion, physical installation, software, and operational contingency management.

중복 항공전자 설계(Redundant Avionics Design)는 화물 무인항공기(Cargo UAV)에서 개별 컴퓨터, 센서, 통신 링크, 전원 또는 액추에이터(Actuator)에 고장이 발생하더라도 제어된 비행(Controlled Flight)을 유지할 수 있도록 하는 설계이다. 효과적인 중복성(Redundancy)은 단순한 부품 복제가 아니라 독립 채널(Independent Channel), 고장 격리(Fault Containment), 지속적인 상태 감시(Health Monitoring), 결정론적 재구성(Deterministic Reconfiguration)을 요구한다. 목적은 장비 고장 자체를 방지하는 것뿐 아니라 단일 고장이 기체 전체의 제어 상실로 확대되는 것을 방지하는 데 있다.

아키텍처는 먼저 비행 필수 기능(Flight-Critical Function)을 식별하고, 이를 유지하기 위해 몇 개의 독립적인 경로가 필요한지를 결정하는 것에서 시작한다. 비행 제어, 항법, 추진 제어, 전력, 통신, 핵심 센싱(Essential Sensing)은 각각의 고장 결과에 따라 서로 다른 중복 전략(Redundancy Strategy)이 필요할 수 있다. 상당한 화물을 운송하는 화물 무인항공기는 제어되지 않은 비행으로 인한 잠재적 피해가 훨씬 크기 때문에 일반적인 소형 무인항공기보다 높은 수준의 고장 허용성(Fault Tolerance)이 요구된다.

이중 중복(Dual Redundancy)은 동일한 기능을 수행하는 두 개의 채널을 제공하여 한 채널에 명확한 고장이 발생했을 때 다른 채널이 운용을 계속할 수 있도록 한다. 그러나 두 채널의 출력이 서로 다를 경우 어느 결과가 올바른지 항상 판단할 수 있는 것은 아니다. 따라서 매우 중요한 기능에는 세 개의 독립 채널이 유사한 결과를 계산하고 투표 로직(Voting Logic)을 통해 비정상 채널을 식별하는 삼중 모듈 중복(Triple Modular Redundancy, TMR)을 적용할 수 있다.

삼중 중복 비행 제어 컴퓨터(Triple Redundant Flight Control Computer)는 각각 독립적으로 센서 정보를 처리하고, 항공기 상태를 추정하며, 제어 법칙(Control Law)을 실행하고, 액추에이터 명령을 생성할 수 있다. 채널 간 감시(Cross-Channel Monitoring)는 각 채널의 운용 상태와 계산 결과를 지속적으로 비교한다. 하나의 FCC가 사전에 정의된 일치 허용범위를 벗어난 값을 생성하면 해당 채널을 격리하고 정상 채널을 이용하여 운용을 계속하면서 고장을 기록하고 상위 시스템 관리 기능에 알릴 수 있다.

중복성은 센서까지 확장되어야 한다. 여러 컴퓨터가 하나의 공통 센서를 사용하는 구조는 진정한 중복 제어 시스템을 형성하지 못하기 때문이다. 복수의 관성 측정 장치(Inertial Measurement Unit, IMU), 위성항법시스템 수신기(GNSS Receiver), 대기자료 센서(Air-Data Sensor), 고도 정보원 또는 자세 기준(Attitude Reference)이 독립적인 측정값을 제공할 수 있다. 센서 투표(Sensor Voting), 일관성 검사(Consistency Checking), 해석적 중복성(Analytical Redundancy), 모델 기반 추정(Model-Based Estimation)을 통해 예상되는 항공기 거동과 불일치하는 측정값을 탐지하고 신뢰할 수 없는 정보원을 활성 솔루션에서 제외할 수 있다.

항법 중복성(Navigation Redundancy)은 자율 화물 운송에서 특히 중요하다. 위성항법시스템(GNSS)은 매우 정확한 절대 위치를 제공할 수 있지만 간섭, 신호 차단, 재밍(Jamming), 스푸핑(Spoofing), 안테나 고장 등에 의해 성능이 저하될 수 있다. 관성항법(Inertial Navigation)은 외부 신호 없이 단기간 상태 추정을 유지할 수 있으며, 추가적인 항법 정보원을 이용해 누적 오차를 제한할 수 있다. 따라서 항공전자 아키텍처는 하나의 위치 결정 기술에 의존하기보다는 항법을 다중 정보원 상태 추정(Multi-Source State Estimation) 문제로 다루어야 한다.

중복 컴퓨터 사이의 통신 경로 역시 공통 고장점(Common Point of Failure)을 만들지 않도록 설계해야 한다. 핵심 데이터에는 독립적인 버스, 스위치, 네트워크 인터페이스, 커넥터, 하니스 경로(Harness Route)가 필요할 수 있다. ARINC 429, ARINC 664/AFDX, MIL-STD-1553, 시간 결정형 이더넷(Time-Triggered Ethernet)과 같은 항공우주 통신 기술은 서로 다른 중복 모델을 지원할 수 있지만, 프로토콜 중복성은 물리적·논리적 네트워크 아키텍처가 적절한 고장 격리를 제공할 때 비로소 효과를 발휘한다.

전기적 중복성(Electrical Redundancy)은 연산 중복성(Computational Redundancy)과 분리할 수 없다. 두 개의 FCC가 동일한 보호되지 않은 전원 레일(Power Rail)에 연결되어 있다면 하나의 전기적 고장으로 두 장치 모두 정지할 수 있다. 따라서 핵심 항공전자 채널은 독립적이거나 적절히 격리된 전원 영역(Power Domain)에 분산하고, 별도의 보호, 전력 변환, 감시, 백업 기능을 제공해야 한다. 배터리 백업 필수 버스(Battery-Backed Essential Bus) 또는 대체 에너지원은 주 전기 시스템의 성능이 저하된 이후에도 최소한의 비행 제어 기능을 유지할 수 있게 한다.

물리적 분리(Physical Separation)는 공통 원인 고장(Common-Cause Failure)을 더욱 감소시킨다. 중복 컴퓨터를 동일한 위치에 설치하면 화재, 침수, 충격 손상, 과열, 전자기 간섭(Electromagnetic Interference), 커넥터 고장 등에 동시에 영향을 받을 수 있다. 동일한 취약 위치를 통과하도록 배치된 센서 배선과 네트워크 하니스 역시 같은 문제를 가질 수 있다. 따라서 중복 항공전자 설계에서는 장비 배치, 하니스 라우팅, 열 구역(Thermal Zone), 접지, 차폐, 커넥터 독립성, 구조적 분리를 시스템 안전 설계의 일부로 고려한다.

고장 감지, 격리 및 복구(Fault Detection, Isolation and Recovery)는 중복 아키텍처 운용의 핵심을 구성한다. 고장 감지(Fault Detection)는 비정상 상태의 존재를 확인하고, 고장 격리(Fault Isolation)는 영향을 받은 부품이나 채널을 식별하며, 복구(Recovery)는 남아 있는 자원을 이용하여 적절한 시스템 구성을 설정한다. 특히 이륙, 착륙, 천이(Transition) 또는 기타 동적으로 민감한 비행 단계에서는 재구성이 수행되는 동안에도 항공기가 제어 가능한 비행 영역(Controllable Flight Envelope) 내에 유지될 수 있을 정도로 빠르게 이러한 기능이 동작해야 한다.

중복 관리(Redundancy Management)는 일시적 고장(Transient Fault)과 지속적인 고장(Persistent Failure)을 구분해야 한다. 일시적인 통신 타임아웃이나 센서 이상이 반드시 해당 채널의 영구적인 제거를 의미하는 것은 아니지만, 반복되거나 물리적으로 불가능한 거동은 격리가 필요할 수 있다. 따라서 상태 감시 로직(Health-Monitoring Logic)은 시간 임계값, 타당성 검사(Plausibility Check), 불일치 카운터, 내장 시험(Built-In Test), 감시 타이머(Watchdog), 통신 감시, 신뢰도 지표(Confidence Metric)를 이용하여 부품을 계속 활성화할지, 재시작할지, 대기 상태로 전환할지 또는 분리할지를 판단할 수 있다.

액추에이터 중복성(Actuator Redundancy)은 연산 명령이 최종적으로 물리적인 제어 권한(Control Authority)에 의존하기 때문에 또 다른 수준의 복잡성을 발생시킨다. 기존 항공기는 중복 서보(Redundant Servo) 또는 조종면을 사용할 수 있으며, 분산 추진 무인항공기는 복수의 모터 또는 로터를 활용할 수 있다. 하나의 액추에이터나 추진 장치가 고장 나더라도 충분한 추력과 제어 권한이 남아 있다면 제어 할당 알고리즘(Control-Allocation Algorithm)이 나머지 장치에 명령을 재분배하여 안전한 비행 상태를 유지할 수 있다.

따라서 분산 추진 아키텍처(Distributed Propulsion Architecture)는 모든 추진 장치에 동일한 예비 장치를 하나씩 배치하지 않더라도 기능적 중복성(Functional Redundancy)을 제공할 수 있다. 중요한 요구사항은 정의된 고장 이후에도 기체 수준의 제어 가능성(Vehicle-Level Controllability)을 확보하는 것이다. FCC는 액추에이터 가용성, 성능 한계, 포화(Saturation), 비대칭 추력(Asymmetric Thrust), 성능이 저하된 동역학을 이해하고 정상 자원에만 명령을 할당하여 항공기가 축소되었지만 안전한 운용 영역 안에 유지되도록 해야 한다.

중복 비행 관리 컴퓨터(Redundant Flight Management Computer)는 FCC와 다른 시간 범위를 대상으로 한다. FMC의 고장이 FCC에서 수행되는 고주기 안정화(High-Rate Stabilization)를 중단시켜서는 안 된다. 대기 또는 병렬 FMC(Standby or Parallel FMC)는 비행 계획, 항법 목표, 임무 상태, 에너지 정보, 비상 대응 데이터를 유지할 수 있다. 활성 FMC에 고장이 발생하면 다른 채널이 임무 관리 권한을 인계받고, 전환 과정에서 FCC는 가장 최근에 검증된 비행 모드나 궤적을 계속 실행할 수 있다.

화물 시스템(Cargo System)의 상태가 비행 안전에 영향을 주는 경우 해당 시스템 역시 중복 관리에 참여해야 한다. 탑재화물 질량(Payload Mass), 무게중심(Center of Gravity), 화물 고정 상태(Cargo Restraint), 도어 또는 잠금 상태 등은 항공기 운용 한계를 변경할 수 있다. 따라서 안전과 관련된 화물 정보에는 독립적인 센싱 또는 타당성 검사가 필요할 수 있다. 잘못된 화물 측정값이 부적절한 궤적, 성능, 에너지 또는 비행 영역 계산으로 이어지기 전에 이를 탐지해야 한다.

지상 통신(Ground Communication)은 유용한 감독 기능을 제공할 수 있지만 탑재 비행 제어를 위한 최종 중복 수단이 되어서는 안 된다. 지상통제소(Ground Control Station, GCS) 또는 데이터링크(Datalink)가 상실되더라도 항공기가 스스로 안정화할 수 있는 능력이 사라져서는 안 된다. 자율 비상 대응 로직(Autonomous Contingency Logic)은 임무 단계, 항공기 상태, 가용 에너지, 기상 제약, 사전에 정의된 운용 규칙에 따라 비행 지속, 선회 대기(Loiter), 복귀(Return), 우회(Diversion), 착륙 등의 통신 두절 대응을 정의해야 한다.

중복성은 공통 모드 고장(Common-Mode Failure)과 공통 원인 고장(Common-Cause Failure)에 대한 보호도 필요로 한다. 세 개의 동일한 컴퓨터를 설치하더라도 모두 동일한 체계적 설계 결함(Systematic Design Defect)을 포함하거나, 동일한 손상 데이터를 수신하거나, 하나의 클록에 의존하거나, 동일한 전력 변환기를 사용하거나, 동일하게 잘못된 소프트웨어 가정을 실행한다면 독립성이 보장되지 않는다. 아키텍처 다양성(Architectural Diversity), 독립 감시, 파티셔닝, 개발 보증(Development Assurance), 엄격하게 관리되는 인터페이스를 통해 하나의 원인이 여러 중복 채널을 동시에 무력화할 가능성을 줄일 수 있다.

점진적 성능 저하(Graceful Degradation)는 핵심적인 설계 원칙이다. 중복 화물 무인항공기를 완전 정상 또는 완전 고장의 두 가지 상태만 존재하는 시스템으로 보아서는 안 된다. 하나의 부품을 상실하면 임무 능력은 감소할 수 있지만 안전한 비행은 계속 유지할 수 있다. 시스템은 중복 자원이 소모됨에 따라 속도, 기동, 고도, 경로 선택, 자율 기능 또는 화물 운용을 단계적으로 제한하고, 남아 있는 안전 여유(Safety Margin)가 부족해지면 최종적으로 우회 또는 비상 착륙으로 전환할 수 있다.

내장 시험(Built-In Test)과 정비 기능(Maintenance Function)은 중복성의 전체 수명주기를 완성한다. 전원 인가 시험(Power-On Test), 지속적인 상태 감시, 정비 진단, 고장 이력, 이벤트 로그, 채널 성능 기록을 이용하면 또 다른 고장이 발생하기 전에 잠재 고장(Latent Failure)을 발견할 수 있다. 특히 감지되지 않은 대기 채널의 고장은 중복성을 조용히 상실하게 만들 수 있으므로 중요하다. 따라서 정비 시스템은 현재 활성화된 장비뿐 아니라 비정상 상황에서만 사용될 수 있는 예비 구성요소까지 검증해야 한다.

전체 Volume 18 구조에서는 중복 항공전자 설계(Redundant Avionics Design)를 FCC/FMC 아키텍처(FCC/FMC Architecture), DO-254 하드웨어 설계(DO-254 Hardware Design), 항공전자 전원 아키텍처(Avionics Power Architecture), 냉각(Cooling), 비행 제어 중복성(Flight-Control Redundancy), 페일세이프 설계(Failsafe Design), 지상통제소 중복 설계(Ground Control Station Redundancy), 무인항공기 안전 아키텍처(UAV Safety Architecture)와 연계하여 구성하고 있다. 이는 중복성이 하나의 항공전자 기능이 아니라 연산, 센싱, 네트워크, 전원, 추진, 물리적 설치, 소프트웨어, 운용 비상 대응 관리 전체에 걸쳐 형성되는 시스템 수준의 특성(System-Level Property)임을 보여준다.

##  

## 02.03. DO-254 Hardware Design

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

DO-254 provides a structured design-assurance framework for airborne electronic hardware whose failure could affect aircraft safety. In a cargo UAV, its principles are particularly relevant to complex electronic hardware used inside Flight Control Computers, Flight Management Computers, sensor interfaces, network controllers, propulsion-control electronics, and other avionics equipment. The central objective is to establish evidence that hardware performs its intended functions correctly and predictably.

Hardware assurance begins with system-level safety requirements rather than with schematic capture or component selection. Aircraft functions are analyzed to determine the consequences of hardware failure, and the resulting safety objectives are allocated to avionics equipment. Hardware requirements must then define precisely what each device or circuit is expected to perform, including functional behavior, interfaces, timing, initialization, monitoring, fault responses, and environmental operating constraints.

The required level of design assurance depends on the severity of the failure condition associated with the hardware function. Functions whose failure could contribute to catastrophic aircraft consequences require substantially stronger development and verification rigor than hardware associated with minor operational effects. This safety-driven classification influences planning, requirements traceability, independence of verification, configuration control, process assurance, and the amount of objective evidence required throughout development.

A fundamental distinction exists between simple and complex electronic hardware. Simple hardware can be comprehensively verified through deterministic analysis and testing without requiring extensive internal design assurance. Complex devices such as FPGAs, programmable logic, highly integrated digital circuits, or sophisticated custom hardware cannot generally be verified solely by testing every possible internal condition. Their development therefore requires systematic requirements, design, implementation, verification, and traceability activities.

Planning establishes how the hardware lifecycle will be controlled before detailed implementation progresses. Development processes, verification methods, configuration management, process assurance, certification evidence, tools, standards, and responsibilities should be defined consistently. For a cargo UAV program, this planning activity is especially important because FCC, FMC, communication, propulsion, power, and sensor electronics may be developed by different teams or suppliers while still contributing to one integrated safety architecture.

Hardware requirements provide the formal bridge between aircraft-level functions and electronic implementation. Requirements should be clear, verifiable, internally consistent, and sufficiently detailed to support design decisions. Inputs and outputs, electrical characteristics, timing behavior, data integrity, reset behavior, fault detection, redundancy interfaces, power transitions, and communication responses may all become hardware requirements. Ambiguous requirements create verification gaps that become increasingly expensive to resolve later.

Conceptual design transforms these requirements into an implementable hardware architecture. Processing devices, memories, communication interfaces, clocks, power supplies, monitoring circuits, sensor interfaces, programmable logic, and discrete electronics are partitioned according to functional and safety needs. Redundant channels should be designed so that independence is preserved wherever required, avoiding hidden common dependencies that could defeat the fault-tolerance objectives of the overall avionics architecture.

Detailed design defines how the conceptual architecture is physically realized. Schematics, programmable logic descriptions, component specifications, interface circuits, clock structures, reset networks, memory organization, PCB constraints, power distribution, and monitoring mechanisms must remain consistent with allocated requirements. Design decisions should be sufficiently documented so that verification engineers can determine not merely that the hardware operates, but why its implementation satisfies each applicable requirement.

Implementation converts the detailed design into physical electronic hardware and programmed devices. PCB layout, FPGA synthesis, device programming, component assembly, manufacturing data, and production configuration become controlled engineering outputs. At this stage, unintended implementation characteristics such as routing-induced timing problems, power integrity limitations, thermal concentration, electromagnetic coupling, or incorrect programmable-device constraints can invalidate assumptions established during earlier design activities.

Requirements traceability connects system requirements, hardware requirements, design elements, implementation outputs, and verification evidence. Bidirectional traceability helps demonstrate that every required function has been implemented and verified while also identifying design features that have no justified requirement. In safety-critical avionics, this discipline prevents undocumented functionality from entering the product and makes design changes easier to evaluate for their effects across the hardware lifecycle.

Verification must demonstrate that the hardware satisfies its requirements under normal, boundary, abnormal, and relevant failure conditions. Review, analysis, simulation, laboratory testing, timing analysis, interface verification, robustness testing, and programmable-logic verification may be combined according to the hardware type. Verification should challenge assumptions and boundary conditions rather than simply demonstrate successful nominal operation, particularly for hardware supporting flight-control and redundancy functions.

Verification independence becomes increasingly important as hardware criticality rises. The engineer who created a design may understand it deeply, but that familiarity can also make hidden assumptions more difficult to detect. Independent review and verification provide another technical perspective on requirements interpretation, implementation correctness, test completeness, and unexpected behavior. Independence therefore functions as a systematic defense against development errors rather than merely an administrative separation of responsibilities.

Programmable logic requires particular attention because FPGA behavior is simultaneously hardware-like and configuration-defined. Logic requirements, clock-domain crossings, reset behavior, state machines, arithmetic behavior, resource utilization, timing closure, fault responses, and interfaces must be verified systematically. Simulation alone may be insufficient, so static analysis, timing analysis, hardware testing, coverage assessment, and implementation reviews can collectively provide evidence that the programmed device behaves as intended.

Clock and reset architectures are safety-relevant because failures in these functions can affect large portions of an avionics computer simultaneously. Independent clock monitoring, startup sequencing, watchdogs, brownout detection, controlled resets, and defined recovery behavior can prevent uncertain electronic states. In redundant FCC architectures, clock or reset dependencies should also be evaluated for common-cause effects so that one infrastructure failure does not unexpectedly disable multiple computational channels.

Power behavior must similarly be addressed throughout hardware design. Avionics electronics experience startup, shutdown, voltage variation, transient disturbances, switching events, and potentially degraded power sources. Hardware should enter defined states during these conditions and recover predictably when valid power returns. Power monitoring, sequencing, isolation, protection, and backup supplies therefore interact directly with DO-254-oriented assurance activities and the broader avionics power architecture described within this volume.

Commercial off-the-shelf devices introduce another assurance challenge because developers may not control their internal design processes. Processors, memories, network devices, converters, and other highly integrated components may contain functionality beyond what the UAV application uses. Their suitability must therefore be supported through appropriate device information, usage constraints, service experience where applicable, verification, architectural mitigation, and system-level monitoring rather than assuming commercial qualification alone establishes airborne suitability.

Tool usage must also be controlled when a development or verification tool can introduce an error or fail to detect one without subsequent independent checking. FPGA synthesis tools, simulation environments, automated test systems, requirement-management platforms, and analysis software may influence assurance evidence. The project must understand how each tool affects lifecycle outputs and determine whether additional verification, tool assessment, or qualification-related activities are necessary for the intended assurance context.

Configuration management ensures that requirements, schematics, programmable logic, PCB data, component lists, verification procedures, test results, and released hardware configurations remain synchronized. A verified FPGA image installed on the wrong PCB revision or an uncontrolled component substitution can invalidate previous evidence. Baselines, change histories, problem reports, release records, and reproducible build information are therefore essential parts of maintaining hardware assurance over the aircraft lifecycle.

Process assurance provides confidence that the planned hardware lifecycle has actually been followed. Reviews and audits identify deviations, incomplete evidence, unresolved problem reports, or inconsistencies between development and verification records. This becomes especially important in large cargo UAV programs involving multiple suppliers because technically capable subsystems can still create certification problems when their lifecycle evidence, configuration records, interfaces, or assurance processes are inconsistent.

DO-254-oriented development should be integrated with redundant avionics design rather than performed after the hardware architecture has already been frozen. Redundant FCCs, FMCs, network channels, power domains, sensor interfaces, and monitoring circuits create assumptions about independence and fault containment that must be reflected in hardware requirements and verification. Assurance evidence must demonstrate not only correct individual operation but also the intended behavior when channels disagree, fail, reset, or transition.

The broader Volume 18 structure places DO-254 hardware design between redundant avionics design and avionics power architecture, while later chapters address flight control, failsafe behavior, redundancy, communication, propulsion, and certification planning. This organization emphasizes that hardware assurance is one layer of a larger cargo UAV safety architecture. Reliable airborne electronics ultimately depend on coordinated requirements, implementation, verification, redundancy, power, communication, configuration control, and system-level validation.

DO-254는 항공기 안전에 영향을 미칠 수 있는 항공 전자 하드웨어(Airborne Electronic Hardware)를 위한 체계적인 설계 보증 프레임워크(Design-Assurance Framework)를 제공한다. 화물 무인항공기(Cargo UAV)에서는 비행 제어 컴퓨터(Flight Control Computer, FCC), 비행 관리 컴퓨터(Flight Management Computer, FMC), 센서 인터페이스, 네트워크 제어기, 추진 제어 전자장치 및 기타 항공전자 장비 내부의 복잡한 전자 하드웨어에 이러한 원칙이 특히 중요하다. 핵심 목적은 하드웨어가 의도된 기능을 정확하고 예측 가능하게 수행한다는 객관적 증거를 확립하는 것이다.

하드웨어 보증(Hardware Assurance)은 회로도 작성이나 부품 선정이 아니라 시스템 수준의 안전 요구사항(System-Level Safety Requirement)에서 시작한다. 항공기 기능을 분석하여 하드웨어 고장이 초래할 수 있는 결과를 결정하고, 그에 따른 안전 목표(Safety Objective)를 항공전자 장비에 할당한다. 이후 하드웨어 요구사항은 각 장치나 회로가 수행해야 하는 기능적 동작, 인터페이스, 타이밍, 초기화, 감시, 고장 대응, 환경 운용 제약을 명확하게 정의해야 한다.

필요한 설계 보증 수준(Design Assurance Level)은 해당 하드웨어 기능과 관련된 고장 상태(Failure Condition)의 심각도에 따라 결정된다. 고장이 항공기에 치명적인 결과를 초래할 수 있는 기능은 경미한 운용 영향만을 발생시키는 하드웨어보다 훨씬 엄격한 개발 및 검증 수준이 요구된다. 이러한 안전 중심 분류는 계획, 요구사항 추적성(Requirements Traceability), 검증 독립성(Verification Independence), 형상 관리(Configuration Control), 프로세스 보증(Process Assurance), 개발 전 과정에서 요구되는 객관적 증거의 수준에 영향을 준다.

단순 전자 하드웨어(Simple Electronic Hardware)와 복합 전자 하드웨어(Complex Electronic Hardware) 사이에는 근본적인 차이가 있다. 단순 하드웨어는 광범위한 내부 설계 보증 절차 없이도 결정론적 분석과 시험을 통해 충분히 검증할 수 있다. 반면 FPGA, 프로그래머블 로직(Programmable Logic), 고집적 디지털 회로, 복잡한 주문형 하드웨어는 가능한 모든 내부 상태를 시험하는 것만으로 검증하기 어렵다. 따라서 체계적인 요구사항, 설계, 구현, 검증, 추적성 활동이 필요하다.

계획 수립(Planning)은 상세 구현이 진행되기 전에 하드웨어 수명주기(Hardware Lifecycle)를 어떻게 통제할 것인지를 정의한다. 개발 프로세스, 검증 방법, 형상 관리, 프로세스 보증, 인증 증거(Certification Evidence), 도구, 표준, 책임을 일관되게 정의해야 한다. 화물 무인항공기 프로그램에서는 FCC, FMC, 통신, 추진, 전력, 센서 전자장치가 서로 다른 팀이나 공급업체에 의해 개발될 수 있으면서도 하나의 통합 안전 아키텍처(Integrated Safety Architecture)를 구성하므로 이러한 계획 활동이 특히 중요하다.

하드웨어 요구사항(Hardware Requirement)은 항공기 수준의 기능과 전자장치 구현 사이를 연결하는 공식적인 연결 고리를 제공한다. 요구사항은 명확하고 검증 가능하며 내부적으로 일관되고 설계 결정을 지원할 수 있을 정도로 상세해야 한다. 입출력, 전기적 특성, 타이밍 동작, 데이터 무결성(Data Integrity), 리셋 동작, 고장 감지, 중복 인터페이스, 전원 천이(Power Transition), 통신 응답 등이 모두 하드웨어 요구사항이 될 수 있다. 모호한 요구사항은 검증 공백을 만들고 개발 후반으로 갈수록 해결 비용을 증가시킨다.

개념 설계(Conceptual Design)는 이러한 요구사항을 구현 가능한 하드웨어 아키텍처로 변환한다. 프로세서, 메모리, 통신 인터페이스, 클록, 전원 공급장치, 감시 회로, 센서 인터페이스, 프로그래머블 로직, 개별 전자회로(Discrete Electronics)는 기능 및 안전 요구에 따라 파티셔닝(Partitioning)된다. 중복 채널(Redundant Channel)은 필요한 독립성이 유지되도록 설계해야 하며, 전체 항공전자 아키텍처의 고장 허용 목표(Fault-Tolerance Objective)를 무력화할 수 있는 숨겨진 공통 의존성을 피해야 한다.

상세 설계(Detailed Design)는 개념 아키텍처를 실제 전자 하드웨어로 구현하는 방법을 정의한다. 회로도, 프로그래머블 로직 기술(Programmable Logic Description), 부품 사양, 인터페이스 회로, 클록 구조, 리셋 네트워크, 메모리 구성, PCB 제약조건, 전력 분배, 감시 메커니즘은 할당된 요구사항과 일관성을 유지해야 한다. 설계 결정은 검증 엔지니어가 단순히 하드웨어의 동작 여부뿐 아니라 구현이 각각의 적용 요구사항을 충족하는 이유까지 판단할 수 있도록 충분히 문서화되어야 한다.

구현(Implementation)은 상세 설계를 물리적인 전자 하드웨어와 프로그래밍된 장치로 변환한다. PCB 레이아웃, FPGA 합성(FPGA Synthesis), 장치 프로그래밍, 부품 조립, 제조 데이터, 생산 형상(Production Configuration)이 통제된 엔지니어링 산출물이 된다. 이 단계에서는 배선에 따른 타이밍 문제, 전원 무결성(Power Integrity) 한계, 열 집중, 전자기 결합(Electromagnetic Coupling), 잘못된 프로그래머블 장치 제약조건 등 의도하지 않은 구현 특성이 이전 설계 단계에서 수립된 가정을 무효화할 수 있다.

요구사항 추적성(Requirements Traceability)은 시스템 요구사항, 하드웨어 요구사항, 설계 요소, 구현 산출물, 검증 증거(Verification Evidence)를 서로 연결한다. 양방향 추적성(Bidirectional Traceability)은 요구된 모든 기능이 구현되고 검증되었음을 입증하는 동시에 정당한 요구사항이 존재하지 않는 설계 기능을 식별하는 데 도움을 준다. 안전 필수 항공전자 시스템에서는 이러한 규율을 통해 문서화되지 않은 기능이 제품에 포함되는 것을 방지하고 설계 변경이 전체 하드웨어 수명주기에 미치는 영향을 쉽게 평가할 수 있다.

검증(Verification)은 정상 조건, 경계 조건(Boundary Condition), 비정상 조건, 관련 고장 조건에서 하드웨어가 요구사항을 만족한다는 것을 입증해야 한다. 하드웨어 유형에 따라 검토, 분석, 시뮬레이션, 실험실 시험, 타이밍 분석, 인터페이스 검증, 강건성 시험(Robustness Testing), 프로그래머블 로직 검증 등을 조합할 수 있다. 특히 비행 제어와 중복 기능을 지원하는 하드웨어에서는 정상 동작만 입증하는 것이 아니라 설계 가정과 경계 조건에 대한 적극적인 검증이 필요하다.

하드웨어 중요도(Criticality)가 높아질수록 검증 독립성(Verification Independence)의 중요성도 증가한다. 설계를 수행한 엔지니어는 해당 설계를 깊이 이해하고 있지만 이러한 익숙함 때문에 숨겨진 가정을 발견하기 어려울 수도 있다. 독립적인 검토와 검증은 요구사항 해석, 구현 정확성, 시험 완전성, 예상하지 못한 동작에 대해 또 다른 기술적 관점을 제공한다. 따라서 독립성은 단순한 행정적 역할 분리가 아니라 개발 오류에 대한 체계적인 방어 수단으로 기능한다.

프로그래머블 로직(Programmable Logic)은 동작 특성이 하드웨어적이면서 동시에 설정에 의해 정의되기 때문에 특별한 주의가 필요하다. 로직 요구사항, 클록 도메인 교차(Clock-Domain Crossing), 리셋 동작, 상태 머신(State Machine), 산술 동작, 자원 사용률, 타이밍 클로저(Timing Closure), 고장 대응, 인터페이스를 체계적으로 검증해야 한다. 시뮬레이션만으로 충분하지 않을 수 있으므로 정적 분석(Static Analysis), 타이밍 분석, 실제 하드웨어 시험, 커버리지 평가(Coverage Assessment), 구현 검토를 결합하여 프로그래밍된 장치가 의도대로 동작한다는 증거를 확보할 수 있다.

클록 및 리셋 아키텍처(Clock and Reset Architecture)는 해당 기능의 고장이 항공전자 컴퓨터의 넓은 영역에 동시에 영향을 줄 수 있기 때문에 안전과 직접 관련된다. 독립 클록 감시, 기동 순서 제어(Startup Sequencing), 감시 타이머(Watchdog), 저전압 감지(Brownout Detection), 제어된 리셋, 정의된 복구 동작을 통해 불확실한 전자 상태를 방지할 수 있다. 중복 FCC 아키텍처에서는 하나의 기반 기능 고장이 여러 연산 채널을 동시에 정지시키지 않도록 클록 또는 리셋 의존성에 대한 공통 원인 영향(Common-Cause Effect)도 평가해야 한다.

전원 동작(Power Behavior) 역시 하드웨어 설계 전체에서 고려되어야 한다. 항공전자 장치는 기동, 종료, 전압 변동, 과도 현상(Transient Disturbance), 스위칭 이벤트, 성능이 저하된 전원 상태를 경험할 수 있다. 이러한 조건에서 하드웨어는 정의된 상태로 진입하고 정상 전원이 복구되었을 때 예측 가능한 방식으로 회복해야 한다. 따라서 전원 감시, 시퀀싱(Sequencing), 격리, 보호, 백업 전원은 DO-254 기반 보증 활동 및 본 권에서 다루는 전체 항공전자 전원 아키텍처(Avionics Power Architecture)와 직접적으로 연계된다.

상용 기성품(Commercial Off-The-Shelf, COTS)은 개발자가 내부 설계 프로세스를 직접 통제할 수 없다는 점에서 또 다른 보증 과제를 발생시킨다. 프로세서, 메모리, 네트워크 장치, 변환기, 기타 고집적 부품에는 UAV 애플리케이션에서 사용하지 않는 기능이 포함될 수 있다. 따라서 상용 인증만으로 항공기 적용 적합성을 가정해서는 안 되며, 적절한 장치 정보, 사용 제약, 적용 가능한 경우의 운용 경험, 검증, 아키텍처적 완화(Architectural Mitigation), 시스템 수준 감시를 통해 적합성을 뒷받침해야 한다.

개발 또는 검증 도구(Development or Verification Tool)가 오류를 유발하거나 후속 독립 검증 없이 오류를 탐지하지 못할 가능성이 있다면 도구 사용 역시 통제해야 한다. FPGA 합성 도구, 시뮬레이션 환경, 자동 시험 시스템, 요구사항 관리 플랫폼, 분석 소프트웨어 등이 보증 증거에 영향을 미칠 수 있다. 프로젝트는 각 도구가 수명주기 산출물에 어떤 영향을 주는지 이해하고, 의도된 보증 환경에 따라 추가 검증, 도구 평가 또는 도구 적격성(Tool Qualification) 관련 활동이 필요한지를 결정해야 한다.

형상 관리(Configuration Management)는 요구사항, 회로도, 프로그래머블 로직, PCB 데이터, 부품 목록, 검증 절차, 시험 결과, 출시된 하드웨어 형상이 서로 동기화된 상태를 유지하도록 한다. 검증된 FPGA 이미지가 잘못된 PCB 버전에 설치되거나 통제되지 않은 부품 대체가 이루어지면 기존 검증 증거가 무효화될 수 있다. 따라서 기준선(Baseline), 변경 이력, 문제 보고서, 출시 기록, 재현 가능한 빌드 정보는 항공기 수명주기 전체에서 하드웨어 보증을 유지하기 위한 핵심 요소이다.

프로세스 보증(Process Assurance)은 계획된 하드웨어 수명주기가 실제로 준수되었다는 신뢰성을 제공한다. 검토와 감사(Audit)를 통해 절차 이탈, 불완전한 증거, 미해결 문제 보고서, 개발 및 검증 기록 사이의 불일치를 식별한다. 여러 공급업체가 참여하는 대형 화물 무인항공기 프로그램에서는 기술적으로 우수한 서브시스템이라도 수명주기 증거, 형상 기록, 인터페이스 또는 보증 프로세스가 서로 일관되지 않으면 인증 문제를 발생시킬 수 있기 때문에 특히 중요하다.

DO-254 기반 개발은 하드웨어 아키텍처가 이미 확정된 이후 별도로 수행하는 것이 아니라 중복 항공전자 설계(Redundant Avionics Design)와 통합되어야 한다. 중복 FCC, FMC, 네트워크 채널, 전원 영역, 센서 인터페이스, 감시 회로는 독립성과 고장 격리에 관한 가정을 형성하며, 이러한 가정은 하드웨어 요구사항과 검증에 반영되어야 한다. 보증 증거는 개별 장치가 올바르게 동작한다는 것뿐 아니라 채널 간 불일치, 고장, 리셋 또는 전환 상황에서 시스템이 의도된 방식으로 동작한다는 것까지 입증해야 한다.

Volume 18의 전체 구조에서는 DO-254 하드웨어 설계(DO-254 Hardware Design)를 중복 항공전자 설계(Redundant Avionics Design)와 항공전자 전원 아키텍처(Avionics Power Architecture) 사이에 배치하고 있으며, 이후 장에서는 비행 제어, 페일세이프 동작(Failsafe Behavior), 중복성, 통신, 추진, 인증 계획(Certification Planning)을 다룬다. 이러한 구성은 하드웨어 보증이 더 큰 화물 무인항공기 안전 아키텍처(Cargo UAV Safety Architecture)의 한 계층임을 강조한다. 신뢰할 수 있는 항공 전자장치는 궁극적으로 요구사항, 구현, 검증, 중복성, 전원, 통신, 형상 관리, 시스템 수준 검증(System-Level Validation)의 긴밀한 연계를 통해 완성된다.

##  

## 02.04. Avionics Power Architecture

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

The avionics power architecture of a cargo UAV provides controlled, reliable, and fault-tolerant electrical energy to flight-critical computers, navigation sensors, communication equipment, monitoring electronics, and control interfaces. Its purpose extends beyond voltage conversion and distribution. The architecture must preserve essential avionics functions during normal operation, electrical transients, source failures, switching events, and progressively degraded aircraft conditions.

Power requirements originate from the avionics functional architecture. Flight Control Computers, Flight Management Computers, GNSS receivers, IMUs, air-data systems, communication interfaces, network switches, cargo-monitoring electronics, and safety controllers have different voltage, current, transient, and availability requirements. These loads must therefore be classified according to functional criticality before electrical buses, converters, protection devices, and backup sources are allocated.

A fundamental design principle is separation between propulsion power and avionics power. Electric or hybrid cargo UAVs can contain high-power motors, inverters, generators, batteries, and switching converters that generate substantial electrical disturbances. Flight-critical avionics require a cleaner and more tightly controlled electrical environment. Isolation, filtering, dedicated conversion stages, grounding strategy, shielding, and appropriate physical separation help prevent propulsion disturbances from propagating into sensitive electronics.

The power architecture commonly establishes multiple distribution levels rather than supplying every avionics device directly from the main energy source. A high-voltage propulsion bus may feed isolated DC/DC converters that create lower-voltage avionics buses, while additional point-of-load converters generate voltages required by processors, FPGAs, sensors, memories, and communication circuits. This hierarchy improves voltage regulation, protection coordination, monitoring, and subsystem-level fault containment.

Redundant avionics require corresponding power redundancy. Installing multiple FCC or FMC channels provides limited safety benefit if all channels depend on one converter, contactor, fuse, connector, or distribution bus. Independent or sufficiently isolated power paths should therefore supply redundant computational channels. A failure in one source or distribution branch must not automatically remove all computers responsible for stabilization, navigation, or mission management.

Essential and nonessential loads should be separated according to their contribution to continued safe flight. Essential loads can include minimum flight-control computation, inertial sensing, required navigation sources, critical communication, actuator interfaces, and power monitoring. Less critical payload, convenience, or mission equipment can be disconnected when electrical capacity becomes limited. Load shedding allows remaining energy to be concentrated on functions required to stabilize and safely recover the aircraft.

Backup power provides another layer of protection when primary generation or distribution becomes unavailable. Dedicated batteries, isolated reserve buses, or alternative generation sources can maintain critical avionics for a defined duration. Backup capacity should be based on the time required to detect the failure, reconfigure the aircraft, establish a safe trajectory, reach an alternate landing location, or perform an emergency landing rather than being treated as an arbitrary energy reserve.

Power source diversity becomes increasingly important in hybrid cargo UAVs. Batteries, generators, fuel cells, turbine-electric systems, or other sources may coexist within the aircraft. Although propulsion energy management is addressed separately within the hybrid power architecture, avionics power design must determine which sources can support essential electronics under different failure combinations. Automatic source transfer must occur without producing unacceptable interruptions or unstable voltage conditions.

Power conversion devices are themselves potential single points of failure. DC/DC converters, voltage regulators, power controllers, contactors, and solid-state switching devices therefore require appropriate redundancy, derating, protection, and health monitoring. Parallel or independent conversion paths can improve availability, but their architecture must prevent one failed converter from collapsing a shared output bus or feeding damaging energy backward into another healthy power channel.

Protection coordination limits the propagation of electrical faults. Fuses, circuit breakers, electronic protection devices, current limiting, overvoltage protection, reverse-current protection, and isolation switches should disconnect the smallest practical affected region. A short circuit in a noncritical sensor or communication unit should not remove the entire avionics bus. Selective protection therefore contributes directly to fault containment and overall aircraft availability.

Power sequencing is particularly important for modern avionics computers containing processors, GPUs, FPGAs, memories, network devices, and multiple voltage rails. Incorrect startup or shutdown sequences can create undefined states even when the nominal supply voltage is correct. Controlled sequencing, power-good signals, reset coordination, brownout detection, and defined initialization behavior ensure that avionics equipment enters and leaves operation predictably.

Voltage transients and interruptions must be considered as normal design challenges rather than exceptional laboratory events. Motor switching, contactor operation, generator transitions, regenerative events, load changes, wiring inductance, and source transfer can generate dips, surges, ripple, and high-frequency disturbances. Filtering, transient suppression, energy storage, converter control, and robust interface design prevent these events from causing computer resets, corrupted data, or erroneous sensor measurements.

Power monitoring transforms the electrical distribution system into an observable avionics subsystem. Voltage, current, temperature, insulation condition, converter status, battery state, contactor state, and protection events can be continuously measured. These measurements allow health-management functions to identify abnormal trends, distinguish local equipment faults from source problems, and provide the FCC or FMC with information required for electrical reconfiguration and mission-level decisions.

The FCC must retain sufficient power information to protect immediate flight safety. Loss of an avionics power channel may require transfer to another source, isolation of failed equipment, reconfiguration of sensors, or transition to a degraded control mode. The FMC can evaluate the longer-term consequences by considering remaining energy, destination distance, alternate landing sites, mission requirements, and the availability of redundant equipment before deciding whether the mission can continue.

Physical implementation strongly influences electrical independence. Redundant power cables routed together through one vulnerable location can be damaged by the same mechanical event, heat source, or fire. Similarly, redundant converters installed in one thermal zone can experience a common overheating condition. Power architecture therefore includes harness routing, connector selection, equipment placement, cooling, grounding, shielding, structural separation, and environmental protection.

Grounding and electromagnetic compatibility are closely connected to avionics power quality. High-current propulsion equipment can introduce conducted and radiated interference through common impedance, cable coupling, chassis paths, or poorly controlled return currents. Defined grounding topology, controlled return paths, filtering, shielding, bonding, and separation between noisy and sensitive circuits reduce interference while preventing unintended ground loops and unstable reference potentials.

Thermal behavior must also be considered because power conversion efficiency directly affects avionics reliability. Even highly efficient converters generate heat continuously, and redundant power electronics may remain active simultaneously. Temperature monitoring, derating, heat spreading, conduction paths, forced-air or liquid cooling where appropriate, and thermal fault responses should ensure that electrical availability is not compromised by excessive temperature during demanding mission phases.

Cargo systems introduce additional electrical loads whose criticality depends on aircraft configuration and mission. Cargo locks, weight sensors, center-of-gravity monitoring, environmental sensors, payload interfaces, and cargo-control electronics may require continued power during specific phases of flight. The architecture should distinguish safety-relevant cargo functions from optional payload functions so that electrical degradation does not inadvertently disable information required to maintain a safe flight envelope.

Maintenance and diagnostics depend on detailed power-system information. Recorded undervoltage events, overcurrent trips, converter temperatures, source transfers, protection activations, and intermittent resets can reveal developing faults before they become operational failures. Built-in test and event logging are particularly valuable for redundant systems because a latent failure in an unused backup power path can otherwise remain undetected until the primary channel fails.

The power architecture must also support controlled ground operation, maintenance, software loading, and preflight testing. External power can reduce unnecessary consumption of onboard energy, but its connection must not bypass protection or introduce unsafe transients into flight hardware. Ground-power interfaces, maintenance modes, isolation mechanisms, and source-selection logic should therefore be integrated into the same controlled electrical architecture used during flight.

As cargo UAV size progresses from 2.5-ton to 5-ton and ultimately 10-ton classes, electrical architecture becomes increasingly distributed and power-intensive. Larger aircraft introduce more avionics equipment, longer harnesses, greater propulsion power, hybrid energy sources, additional redundancy, and stronger thermal constraints. Power distribution must therefore evolve from a collection of supplies into an actively monitored, fault-contained, reconfigurable electrical network.

Within Volume 18, avionics power architecture follows FCC/FMC architecture, redundant avionics design, and DO-254 hardware design, while the next topic addresses avionics cooling. Later chapters separately cover flight control, failsafe behavior, cargo management, hybrid power systems, and progressively larger cargo UAV classes. This structure positions avionics power as the electrical foundation that allows computing, sensing, communication, redundancy, and safety functions to remain available throughout flight.

화물 무인항공기(Cargo UAV)의 항공전자 전원 아키텍처(Avionics Power Architecture)는 비행 필수 컴퓨터, 항법 센서, 통신 장비, 감시 전자장치 및 제어 인터페이스에 통제되고 신뢰성 높으며 고장 허용성이 있는 전기에너지를 공급한다. 그 목적은 단순한 전압 변환과 분배를 넘어선다. 정상 운용뿐 아니라 전기적 과도현상(Electrical Transient), 전원 고장, 스위칭 이벤트, 단계적으로 성능이 저하되는 항공기 상태에서도 필수 항공전자 기능을 유지해야 한다.

전원 요구사항(Power Requirement)은 항공전자 기능 아키텍처(Avionics Functional Architecture)에서 시작된다. 비행 제어 컴퓨터(Flight Control Computer, FCC), 비행 관리 컴퓨터(Flight Management Computer, FMC), 위성항법시스템(GNSS) 수신기, 관성 측정 장치(Inertial Measurement Unit, IMU), 대기자료 시스템(Air-Data System), 통신 인터페이스, 네트워크 스위치, 화물 감시 전자장치, 안전 제어기는 서로 다른 전압, 전류, 과도현상, 가용성 요구사항을 가진다. 따라서 전기 버스, 변환기, 보호 장치, 백업 전원을 할당하기 전에 기능 중요도(Functional Criticality)에 따라 부하를 분류해야 한다.

기본적인 설계 원칙은 추진 전원(Propulsion Power)과 항공전자 전원(Avionics Power)의 분리이다. 전기식 또는 하이브리드 화물 무인항공기는 상당한 전기적 외란을 발생시키는 고출력 모터, 인버터, 발전기, 배터리, 스위칭 변환기를 포함할 수 있다. 비행 필수 항공전자 장비에는 더욱 깨끗하고 엄격하게 제어된 전기적 환경이 필요하다. 절연(Isolation), 필터링(Filtering), 전용 변환 단계, 접지 전략, 차폐, 적절한 물리적 분리를 통해 추진 계통의 외란이 민감한 전자장치로 전달되는 것을 방지할 수 있다.

전원 아키텍처는 일반적으로 모든 항공전자 장치에 주 에너지원에서 직접 전원을 공급하기보다 여러 단계의 전력 분배 구조를 구성한다. 고전압 추진 버스(High-Voltage Propulsion Bus)가 절연형 직류-직류 변환기(Isolated DC/DC Converter)에 전력을 공급하여 저전압 항공전자 버스를 생성하고, 추가적인 부하점 변환기(Point-of-Load Converter)가 프로세서, FPGA, 센서, 메모리, 통신 회로에 필요한 전압을 생성할 수 있다. 이러한 계층 구조는 전압 조정, 보호 협조(Protection Coordination), 감시, 서브시스템 수준의 고장 격리를 향상시킨다.

중복 항공전자 시스템(Redundant Avionics)은 이에 대응하는 전원 중복성(Power Redundancy)을 필요로 한다. 여러 FCC 또는 FMC 채널을 설치하더라도 모든 채널이 하나의 변환기, 접촉기(Contactor), 퓨즈, 커넥터 또는 분배 버스에 의존한다면 안전성 향상 효과는 제한적이다. 따라서 중복 연산 채널에는 독립적이거나 충분히 격리된 전원 경로를 제공해야 한다. 하나의 전원 또는 분배 분기 고장이 안정화, 항법, 임무 관리를 담당하는 모든 컴퓨터를 동시에 정지시켜서는 안 된다.

필수 부하(Essential Load)와 비필수 부하(Nonessential Load)는 안전한 비행 지속에 대한 기여도에 따라 분리해야 한다. 필수 부하에는 최소 비행 제어 연산, 관성 센싱, 필요한 항법 정보원, 핵심 통신, 액추에이터 인터페이스, 전원 감시 등이 포함될 수 있다. 전력 용량이 제한되면 중요도가 낮은 탑재체, 편의 기능 또는 임무 장비를 차단할 수 있다. 부하 차단(Load Shedding)을 통해 남아 있는 에너지를 항공기 안정화와 안전한 회수에 필요한 기능에 집중할 수 있다.

백업 전원(Backup Power)은 주 발전 또는 전력 분배 기능을 사용할 수 없게 되었을 때 추가적인 보호 계층을 제공한다. 전용 배터리, 절연된 예비 버스(Reserve Bus), 대체 발전원이 정의된 시간 동안 핵심 항공전자 장비를 유지할 수 있다. 백업 용량은 임의의 에너지 예비량으로 결정하기보다 고장을 감지하고, 항공기를 재구성하며, 안전한 궤적을 설정하고, 대체 착륙지에 도달하거나 비상 착륙을 수행하는 데 필요한 시간을 기준으로 결정해야 한다.

전원 다양성(Power Source Diversity)은 하이브리드 화물 무인항공기에서 더욱 중요해진다. 배터리, 발전기, 연료전지(Fuel Cell), 터빈-전기 시스템(Turbine-Electric System) 또는 기타 전원이 하나의 항공기에 공존할 수 있다. 추진 에너지 관리는 별도의 하이브리드 전원 아키텍처(Hybrid Power Architecture)에서 다루더라도, 항공전자 전원 설계에서는 서로 다른 고장 조합에서 어떤 전원이 필수 전자장비를 지원할 수 있는지를 결정해야 한다. 자동 전원 전환(Automatic Source Transfer)은 허용할 수 없는 전원 중단이나 불안정한 전압 상태를 발생시키지 않아야 한다.

전력 변환 장치(Power Conversion Device) 자체도 잠재적인 단일 고장점(Single Point of Failure)이 될 수 있다. 따라서 직류-직류 변환기(DC/DC Converter), 전압 조정기(Voltage Regulator), 전력 제어기, 접촉기, 반도체 스위칭 장치(Solid-State Switching Device)에는 적절한 중복성, 디레이팅(Derating), 보호, 상태 감시가 필요하다. 병렬 또는 독립 변환 경로는 가용성을 향상시킬 수 있지만 하나의 고장 난 변환기가 공통 출력 버스를 붕괴시키거나 정상 전원 채널로 유해한 에너지를 역류시키지 않도록 설계해야 한다.

보호 협조(Protection Coordination)는 전기적 고장이 다른 영역으로 확산되는 것을 제한한다. 퓨즈, 회로 차단기(Circuit Breaker), 전자식 보호 장치, 전류 제한(Current Limiting), 과전압 보호, 역전류 보호, 절연 스위치는 가능한 한 가장 작은 고장 영역만 분리해야 한다. 중요하지 않은 센서나 통신 장치의 단락(Short Circuit)으로 전체 항공전자 버스가 정지해서는 안 된다. 따라서 선택적 보호(Selective Protection)는 고장 격리와 전체 항공기 가용성에 직접적으로 기여한다.

전원 시퀀싱(Power Sequencing)은 프로세서, GPU, FPGA, 메모리, 네트워크 장치 및 여러 전압 레일을 포함하는 현대 항공전자 컴퓨터에서 특히 중요하다. 공칭 공급 전압이 정상이라도 잘못된 기동 또는 종료 순서는 정의되지 않은 상태를 발생시킬 수 있다. 제어된 시퀀싱, 전원 정상 신호(Power-Good Signal), 리셋 조정, 저전압 감지(Brownout Detection), 정의된 초기화 동작을 통해 항공전자 장비가 예측 가능한 방식으로 운용을 시작하고 종료하도록 해야 한다.

전압 과도현상(Voltage Transient)과 순간적인 전원 중단은 예외적인 실험실 현상이 아니라 일반적인 설계 과제로 고려해야 한다. 모터 스위칭, 접촉기 동작, 발전기 전환, 회생 이벤트(Regenerative Event), 부하 변화, 배선 인덕턴스, 전원 전환은 전압 강하, 서지(Surge), 리플(Ripple), 고주파 외란을 발생시킬 수 있다. 필터링, 과도현상 억제(Transient Suppression), 에너지 저장, 변환기 제어, 강건한 인터페이스 설계를 통해 이러한 현상이 컴퓨터 리셋, 데이터 손상 또는 잘못된 센서 측정을 일으키는 것을 방지해야 한다.

전원 감시(Power Monitoring)는 전력 분배 시스템을 관측 가능한 항공전자 서브시스템으로 변환한다. 전압, 전류, 온도, 절연 상태, 변환기 상태, 배터리 상태, 접촉기 상태, 보호 동작 이벤트를 지속적으로 측정할 수 있다. 이러한 측정값을 통해 상태 관리 기능(Health-Management Function)은 비정상적인 경향을 식별하고, 국부적인 장비 고장과 전원 문제를 구분하며, 전기적 재구성과 임무 수준 판단에 필요한 정보를 FCC 또는 FMC에 제공할 수 있다.

FCC는 즉각적인 비행 안전을 보호하는 데 필요한 충분한 전원 정보를 유지해야 한다. 항공전자 전원 채널의 상실은 다른 전원으로의 전환, 고장 장비의 격리, 센서 재구성 또는 성능 저하 제어 모드(Degraded Control Mode)로의 전환을 요구할 수 있다. FMC는 잔여 에너지, 목적지까지의 거리, 대체 착륙지, 임무 요구사항, 중복 장비의 가용성을 고려하여 장기적인 영향을 평가하고 임무 지속 가능 여부를 판단할 수 있다.

물리적 구현(Physical Implementation)은 전기적 독립성에 큰 영향을 준다. 중복 전원 케이블을 동일한 취약 위치를 통과하도록 배선하면 동일한 기계적 손상, 열원 또는 화재로 동시에 손상될 수 있다. 마찬가지로 중복 변환기를 하나의 열 구역(Thermal Zone)에 설치하면 공통 과열 상태가 발생할 수 있다. 따라서 전원 아키텍처는 하니스 라우팅, 커넥터 선정, 장비 배치, 냉각, 접지, 차폐, 구조적 분리, 환경 보호를 포함한다.

접지(Grounding)와 전자기 적합성(Electromagnetic Compatibility, EMC)은 항공전자 전원 품질과 밀접하게 연결되어 있다. 고전류 추진 장비는 공통 임피던스, 케이블 결합, 섀시 경로 또는 제대로 통제되지 않은 귀환 전류(Return Current)를 통해 전도성 및 방사성 간섭을 발생시킬 수 있다. 정의된 접지 토폴로지, 통제된 귀환 경로, 필터링, 차폐, 본딩(Bonding), 노이즈 회로와 민감 회로 사이의 분리를 통해 간섭을 줄이고 의도하지 않은 접지 루프(Ground Loop)와 불안정한 기준 전위를 방지할 수 있다.

전력 변환 효율이 항공전자 신뢰성에 직접적인 영향을 미치므로 열적 거동(Thermal Behavior)도 고려해야 한다. 고효율 변환기라도 지속적으로 열을 발생시키며 중복 전력 전자장치가 동시에 활성화될 수도 있다. 온도 감시, 디레이팅, 열 확산(Heat Spreading), 열전도 경로, 필요한 경우 강제 공랭 또는 액체 냉각, 열 고장 대응을 통해 높은 부하가 요구되는 임무 단계에서도 과도한 온도로 인해 전기적 가용성이 저하되지 않도록 해야 한다.

화물 시스템(Cargo System)은 항공기 구성과 임무에 따라 중요도가 달라지는 추가 전기 부하를 발생시킨다. 화물 잠금 장치, 중량 센서, 무게중심 감시(CG Monitoring), 환경 센서, 탑재체 인터페이스(Payload Interface), 화물 제어 전자장치는 특정 비행 단계에서 지속적인 전원 공급이 필요할 수 있다. 전기 시스템의 성능 저하로 안전한 비행 영역을 유지하는 데 필요한 정보가 의도치 않게 상실되지 않도록 안전 관련 화물 기능과 선택적 탑재체 기능을 구분해야 한다.

정비 및 진단(Maintenance and Diagnostics)은 상세한 전원 시스템 정보에 의존한다. 기록된 저전압 이벤트, 과전류 차단, 변환기 온도, 전원 전환, 보호 장치 작동, 간헐적인 리셋은 운용 고장으로 발전하기 전에 잠재적인 문제를 발견하는 데 도움을 준다. 특히 중복 시스템에서는 사용되지 않는 백업 전원 경로의 잠재 고장(Latent Failure)이 주 채널 고장 시까지 발견되지 않을 수 있으므로 내장 시험(Built-In Test)과 이벤트 기록(Event Logging)이 중요하다.

전원 아키텍처는 통제된 지상 운용, 정비, 소프트웨어 로딩, 비행 전 시험(Preflight Testing)도 지원해야 한다. 외부 전원(External Power)을 사용하면 탑재 에너지의 불필요한 소비를 줄일 수 있지만 외부 전원의 연결이 보호 기능을 우회하거나 비행 하드웨어에 위험한 과도현상을 발생시켜서는 안 된다. 따라서 지상 전원 인터페이스, 정비 모드, 절연 메커니즘, 전원 선택 로직은 비행 중 사용하는 것과 동일한 통제된 전기 아키텍처에 통합되어야 한다.

화물 무인항공기의 규모가 2.5톤급에서 5톤급, 궁극적으로 10톤급으로 증가함에 따라 전기 아키텍처는 더욱 분산되고 고출력화된다. 대형 항공기에는 더 많은 항공전자 장비, 더 긴 하니스, 더 높은 추진 전력, 하이브리드 에너지원, 추가적인 중복성, 더욱 엄격한 열적 제약이 도입된다. 따라서 전력 분배는 단순한 전원장치의 집합에서 능동적으로 감시되고, 고장이 격리되며, 재구성 가능한 전기 네트워크(Reconfigurable Electrical Network)로 발전해야 한다.

Volume 18의 구조에서 항공전자 전원 아키텍처(Avionics Power Architecture)는 FCC/FMC 아키텍처(FCC/FMC Architecture), 중복 항공전자 설계(Redundant Avionics Design), DO-254 하드웨어 설계(DO-254 Hardware Design)에 이어 배치되며, 다음 주제에서는 항공전자 냉각(Avionics Cooling)을 다룬다. 이후 장에서는 비행 제어, 페일세이프 동작(Failsafe Behavior), 화물 관리, 하이브리드 전원 시스템, 단계적으로 대형화되는 화물 무인항공기를 별도로 다룬다. 이러한 구조는 항공전자 전원이 비행 전 과정에서 연산, 센싱, 통신, 중복성, 안전 기능을 지속적으로 사용할 수 있도록 하는 전기적 기반(Electrical Foundation)임을 보여준다.

##  

## 02.05. Avionics Cooling Design

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

Avionics cooling design ensures that flight-critical electronic equipment remains within allowable temperature limits throughout the complete cargo UAV mission. Flight Control Computers, Flight Management Computers, processors, FPGAs, communication devices, power converters, sensor interfaces, and monitoring electronics continuously generate heat. Cooling must therefore be treated as part of avionics reliability and safety architecture rather than as a secondary packaging consideration.

Electronic temperature directly influences component reliability, computational stability, and service life. Excessive junction temperature can accelerate semiconductor degradation, increase leakage current, alter electrical characteristics, reduce power-converter efficiency, and eventually cause shutdown or permanent damage. Even when equipment remains operational, repeated thermal cycling can fatigue solder joints, connectors, PCB structures, and interfaces between electronic components and their cooling surfaces.

Thermal design begins with a heat-load model of the avionics architecture. Each computer, converter, network device, sensor-processing module, and power component contributes a different amount of heat according to operating mode. Peak electrical power alone is insufficient because actual thermal behavior depends on efficiency, duty cycle, mission phase, processor utilization, ambient temperature, airflow, enclosure design, and heat-transfer paths from semiconductor junctions to the external environment.

Cargo UAV missions create highly variable thermal conditions. Ground operation may combine high ambient temperature with little natural airflow, while climb can impose maximum computational and propulsion-related loads. Cruise may improve external airflow but expose equipment to different atmospheric temperatures and pressures. Landing and post-flight operation introduce further transitions. Cooling architecture must therefore address the complete mission thermal profile rather than optimize only for steady cruise conditions.

Passive cooling is attractive because it minimizes moving parts, electrical consumption, acoustic noise, and maintenance requirements. Heat sinks, thermal interface materials, conduction plates, structural heat spreaders, enclosure surfaces, and natural convection can transfer heat without active machinery. Passive methods are especially useful for lower-power avionics, but their capability becomes limited as processor density and internal heat flux increase in advanced autonomous cargo UAV computers.

Conduction cooling transfers heat directly from electronic components and circuit boards into a chassis, cold plate, equipment rack, or aircraft structure. This approach can provide predictable thermal paths while avoiding dependence on internal airflow. Mechanical interfaces become critical because contact pressure, surface flatness, thermal interface materials, mounting tolerances, vibration, and structural deformation can significantly change thermal resistance between the heat-generating device and the final heat sink.

Forced-air cooling increases heat-transfer capability by moving air across heat sinks, circuit boards, or equipment enclosures. Fans and blowers can support processors and power electronics with higher thermal loads, but they introduce additional failure modes. Bearing wear, dust accumulation, blocked passages, filter contamination, reduced air density, and fan-controller faults must be considered. Safety-critical equipment should not lose essential functionality immediately following a single cooling-fan failure.

Airflow architecture requires deliberate management rather than simply installing additional fans. Intake location, exhaust routing, pressure drop, recirculation, equipment spacing, cable obstruction, hot-air mixing, and local stagnation regions influence actual cooling performance. Thermal analysis should identify hotspots inside avionics bays and ensure that downstream equipment is not supplied primarily with air already heated by upstream computers or power-conversion modules.

Liquid cooling becomes attractive when avionics heat density exceeds practical air-cooling capability. Cold plates can collect heat from high-performance processors, GPUs, FPGAs, and power electronics, while pumps circulate coolant toward a heat exchanger or radiator. Liquid systems provide high heat-transfer capacity and flexible heat transport, but introduce pumps, hoses, seals, connectors, reservoirs, coolant compatibility, leakage detection, and additional maintenance considerations.

A redundant avionics architecture requires corresponding consideration of cooling independence. Two redundant FCCs installed on the same cooling loop can experience simultaneous thermal failure if one pump or heat exchanger is lost. Thermal architecture should therefore evaluate whether redundant computers require independent cooling paths, passive emergency capability, multiple pumps, isolated branches, or sufficient thermal inertia to maintain operation while the aircraft transitions to a safe degraded state.

Thermal fault containment is as important as nominal cooling performance. One overheating unit should not unnecessarily raise the temperature of adjacent redundant equipment. Physical separation, thermal barriers, independent heat paths, controlled airflow, compartmentalization, and strategic equipment placement can reduce propagation. This principle complements electrical and computational redundancy by preventing a common thermal event from disabling multiple safety-critical channels.

Temperature sensing provides the feedback required for active thermal management. Semiconductor junction estimates, board sensors, inlet and outlet air temperatures, coolant temperatures, heat-sink sensors, and avionics-bay measurements can reveal both immediate overheating and gradual degradation. Multiple measurement points are valuable because a normal enclosure temperature does not guarantee that a processor junction, voltage regulator, FPGA, or localized PCB region remains within its allowable range.

Thermal monitoring should be integrated with avionics health management rather than remain isolated within cooling hardware. Temperature trends, fan speed, pump status, coolant flow, processor load, converter temperature, and environmental conditions can be combined to estimate remaining thermal margin. The FCC and FMC can then receive relevant health information and determine whether computational capability, mission operation, or aircraft trajectory must be modified.

Graceful thermal degradation can prevent overheating from immediately becoming a flight-critical failure. A high-performance computer may reduce processor or GPU frequency, disable nonessential workloads, lower sensor-processing rates, or suspend optional AI functions while preserving core flight control. Nonessential mission equipment can also be shut down. Thermal management therefore interacts with computational scheduling and electrical load shedding to protect the minimum functions required for safe flight.

The distinction between flight-critical and mission-critical computing is important for cooling allocation. FCC functions require predictable availability and should receive cooling resources consistent with their safety role. Higher-level AI perception, mission optimization, payload processing, or data recording may consume substantially more power but can often tolerate controlled performance reduction. Thermal priorities should reflect functional criticality rather than simply the magnitude of each equipment heat load.

Avionics power architecture and cooling architecture are strongly coupled. Electrical conversion losses become thermal loads, while fans, pumps, valves, and cooling controllers themselves consume electrical power. A degraded electrical system may therefore reduce cooling capability precisely when remaining converters are carrying higher loads. Joint electrical-thermal analysis is required to evaluate realistic failure conditions and avoid assumptions that each architecture independently has unlimited supporting resources.

Environmental conditions introduce additional design constraints. Cargo UAV avionics may encounter high and low ambient temperatures, solar heating, humidity, rain, dust, salt contamination, altitude-related pressure changes, and rapid thermal transitions. Sealed enclosures improve environmental protection but restrict convection. Ventilated systems improve airflow but increase contamination exposure. Cooling design must balance environmental sealing, heat rejection, maintainability, mass, and reliability.

Altitude affects air cooling because reduced air density changes convective heat-transfer performance. A cooling system that performs adequately during ground testing may have less margin at operating altitude, particularly when high computational workloads continue during climb or cruise. Fans and heat exchangers must therefore be evaluated under representative atmospheric conditions, and thermal models should account for changes in air density, temperature, pressure, and aircraft operating state.

Electromagnetic compatibility also interacts with cooling design. Large ventilation openings can weaken enclosure shielding, while fans, pumps, and their electronic drives can introduce electrical noise. Conductive heat paths may simultaneously become grounding or bonding paths. Cooling interfaces must therefore be coordinated with enclosure design, shielding, grounding, filtering, and cable routing so that improved thermal performance does not create new electromagnetic interference or electrical safety problems.

Thermal analysis should combine analytical calculations, simulation, component characterization, and physical testing. Early models can estimate heat paths and equipment temperatures before hardware exists, while detailed computational analysis can identify local airflow or conduction problems. Prototype testing under controlled environmental conditions is then required to validate assumptions, correlate models, and determine whether thermal margins remain adequate under representative loads and failure cases.

Verification must include abnormal conditions rather than demonstrating only nominal cooling. Fan failure, pump degradation, blocked airflow, increased processor load, elevated ambient temperature, partial power-system failure, sensor faults, and degraded heat-transfer interfaces should be considered where relevant. The objective is to determine how quickly temperatures rise, which functions are affected, whether monitoring detects the condition, and how long essential avionics remain operational.

Maintenance strategy should preserve cooling performance throughout the aircraft lifecycle. Fans, filters, pumps, coolant, thermal interface materials, heat exchangers, and ventilation passages can degrade gradually. Temperature trends and cooling-system health records can support predictive maintenance by identifying increasing thermal resistance or declining airflow before operational limits are exceeded. Accessible equipment placement also reduces the cost and risk of inspection and replacement.

As cargo UAVs progress from 2.5-ton to 5-ton and 10-ton classes, avionics cooling becomes increasingly integrated with vehicle-level thermal management. Larger aircraft can carry more powerful computers, redundant electronics, communication systems, hybrid-power controllers, and autonomous processing hardware. Future designs may therefore combine distributed conduction, forced air, liquid cooling, and centralized heat rejection rather than relying on one universal cooling method.

Within Volume 18, avionics cooling design completes the Avionics Architecture chapter after FCC/FMC architecture, redundant avionics design, DO-254 hardware design, and avionics power architecture. The following chapters address aerospace protocols and flight-control systems, while later sections cover hybrid power and progressively larger cargo UAV platforms. This structure establishes cooling as a fundamental enabling layer for reliable computing, redundancy, communication, control, and safe autonomous flight.

항공전자 냉각 설계(Avionics Cooling Design)는 전체 화물 무인항공기(Cargo UAV) 임무 동안 비행 필수 전자장비가 허용 온도 범위 내에서 유지되도록 한다. 비행 제어 컴퓨터(Flight Control Computer, FCC), 비행 관리 컴퓨터(Flight Management Computer, FMC), 프로세서, FPGA, 통신 장치, 전력 변환기, 센서 인터페이스, 감시 전자장치는 지속적으로 열을 발생시킨다. 따라서 냉각은 부수적인 패키징 고려사항이 아니라 항공전자 신뢰성 및 안전 아키텍처의 일부로 다루어야 한다.

전자장치의 온도는 부품 신뢰성(Component Reliability), 연산 안정성(Computational Stability), 수명(Service Life)에 직접적인 영향을 준다. 과도한 접합부 온도(Junction Temperature)는 반도체 열화를 가속하고 누설 전류를 증가시키며 전기적 특성을 변화시키고 전력 변환기의 효율을 저하시켜 결국 시스템 정지 또는 영구적인 손상을 발생시킬 수 있다. 장비가 계속 동작하더라도 반복적인 열 사이클링(Thermal Cycling)은 솔더 접합부, 커넥터, PCB 구조 및 전자부품과 냉각 표면 사이의 인터페이스에 피로를 누적시킬 수 있다.

열 설계(Thermal Design)는 항공전자 아키텍처의 열 부하 모델(Heat-Load Model)에서 시작한다. 각각의 컴퓨터, 변환기, 네트워크 장치, 센서 처리 모듈, 전력 부품은 운용 모드에 따라 서로 다른 양의 열을 발생시킨다. 최대 전력만으로는 실제 열적 거동을 판단하기에 충분하지 않다. 실제 온도는 효율, 듀티 사이클(Duty Cycle), 임무 단계, 프로세서 사용률, 주변 온도, 공기 흐름, 인클로저 설계, 반도체 접합부에서 외부 환경까지의 열전달 경로에 의해 결정되기 때문이다.

화물 무인항공기의 임무는 매우 다양한 열 환경을 발생시킨다. 지상 운용에서는 높은 주변 온도와 낮은 자연 공기 흐름이 동시에 나타날 수 있으며, 상승 단계에서는 최대 수준의 연산 및 추진 관련 부하가 발생할 수 있다. 순항에서는 외부 공기 흐름이 개선될 수 있지만 서로 다른 대기 온도와 압력에 노출된다. 착륙과 비행 종료 후 운용에서도 추가적인 열적 천이가 발생한다. 따라서 냉각 아키텍처는 정상 순항 조건에만 최적화하기보다 전체 임무 열 프로파일(Mission Thermal Profile)을 고려해야 한다.

수동 냉각(Passive Cooling)은 움직이는 부품, 전력 소비, 소음, 정비 요구사항을 최소화할 수 있다는 장점이 있다. 방열판(Heat Sink), 열 인터페이스 재료(Thermal Interface Material), 전도판(Conduction Plate), 구조적 열 확산기(Structural Heat Spreader), 인클로저 표면, 자연 대류(Natural Convection)를 이용하면 별도의 능동 장치 없이 열을 전달할 수 있다. 수동 방식은 저전력 항공전자 장비에 특히 유용하지만 첨단 자율 화물 UAV 컴퓨터에서 프로세서 밀도와 내부 열유속(Heat Flux)이 증가하면 냉각 능력이 제한될 수 있다.

전도 냉각(Conduction Cooling)은 전자부품과 회로기판에서 발생한 열을 섀시, 콜드 플레이트(Cold Plate), 장비 랙 또는 항공기 구조물로 직접 전달한다. 이 방식은 내부 공기 흐름에 의존하지 않으면서 예측 가능한 열전달 경로를 제공할 수 있다. 그러나 접촉 압력, 표면 평탄도, 열 인터페이스 재료, 조립 공차, 진동, 구조적 변형이 발열 장치와 최종 방열부 사이의 열저항(Thermal Resistance)을 크게 변화시킬 수 있으므로 기계적 인터페이스가 매우 중요하다.

강제 공랭(Forced-Air Cooling)은 방열판, 회로기판 또는 장비 인클로저를 따라 공기를 이동시켜 열전달 능력을 향상시킨다. 팬과 블로어(Blower)를 사용하면 높은 열 부하를 가진 프로세서와 전력 전자장치를 지원할 수 있지만 추가적인 고장 모드가 발생한다. 베어링 마모, 먼지 축적, 공기 통로 막힘, 필터 오염, 공기 밀도 감소, 팬 제어기 고장 등을 고려해야 한다. 안전 필수 장비는 하나의 냉각 팬 고장 직후 필수 기능을 상실하지 않도록 설계해야 한다.

공기 흐름 아키텍처(Airflow Architecture)는 단순히 팬을 추가하는 것이 아니라 체계적으로 관리해야 한다. 흡입구 위치, 배기 경로, 압력 강하, 공기 재순환, 장비 간격, 케이블에 의한 흐름 방해, 고온 공기의 혼합, 국부적인 정체 영역(Local Stagnation Region)이 실제 냉각 성능에 영향을 준다. 열 해석은 항공전자 장비실 내부의 핫스팟(Hotspot)을 식별하고, 하류 장비가 상류 컴퓨터나 전력 변환 모듈에 의해 이미 가열된 공기를 주로 공급받지 않도록 해야 한다.

액체 냉각(Liquid Cooling)은 항공전자 장비의 열 밀도가 실용적인 공랭 능력을 초과할 때 유용하다. 콜드 플레이트는 고성능 프로세서, GPU, FPGA, 전력 전자장치에서 발생한 열을 수집하고 펌프가 냉각수를 열교환기(Heat Exchanger) 또는 라디에이터로 순환시킨다. 액체 냉각은 높은 열전달 용량과 유연한 열 이동 능력을 제공하지만 펌프, 호스, 씰(Seal), 커넥터, 저장 탱크, 냉각수 호환성, 누설 감지 및 추가적인 정비 요구사항을 발생시킨다.

중복 항공전자 아키텍처(Redundant Avionics Architecture)는 냉각 시스템의 독립성(Cooling Independence)도 함께 고려해야 한다. 두 개의 중복 FCC가 동일한 냉각 루프에 설치되어 있다면 하나의 펌프나 열교환기 고장으로 동시에 열적 고장이 발생할 수 있다. 따라서 열 아키텍처에서는 중복 컴퓨터에 독립 냉각 경로, 수동 비상 냉각 능력, 복수 펌프, 격리된 냉각 분기 또는 항공기가 안전한 성능 저하 상태로 전환하는 동안 운용을 유지할 수 있는 충분한 열 관성(Thermal Inertia)이 필요한지를 평가해야 한다.

열적 고장 격리(Thermal Fault Containment)는 정상 냉각 성능만큼 중요하다. 하나의 장비가 과열되었다고 해서 인접한 중복 장비의 온도까지 불필요하게 상승해서는 안 된다. 물리적 분리, 열 차단막(Thermal Barrier), 독립적인 열전달 경로, 통제된 공기 흐름, 구획화(Compartmentalization), 전략적인 장비 배치를 통해 고장 전파를 줄일 수 있다. 이러한 원칙은 공통 열적 사건이 여러 안전 필수 채널을 동시에 정지시키는 것을 방지함으로써 전기적·연산적 중복성을 보완한다.

온도 센싱(Temperature Sensing)은 능동 열 관리(Active Thermal Management)에 필요한 피드백을 제공한다. 반도체 접합부 온도 추정값, 보드 센서, 흡입 및 배출 공기 온도, 냉각수 온도, 방열판 센서, 항공전자 장비실 온도를 통해 즉각적인 과열뿐 아니라 점진적인 성능 저하도 파악할 수 있다. 인클로저 온도가 정상이라고 해서 프로세서 접합부, 전압 조정기, FPGA 또는 국부적인 PCB 영역이 허용 범위 내에 있다는 것을 보장할 수 없으므로 복수의 측정 지점이 중요하다.

열 감시(Thermal Monitoring)는 냉각 하드웨어 내부에 독립적으로 존재하기보다 항공전자 상태 관리(Avionics Health Management)에 통합되어야 한다. 온도 변화 추세, 팬 속도, 펌프 상태, 냉각수 유량, 프로세서 부하, 변환기 온도, 환경 조건을 결합하여 잔여 열 여유(Remaining Thermal Margin)를 추정할 수 있다. 이후 FCC와 FMC가 관련 상태 정보를 수신하여 연산 능력, 임무 운용 또는 항공기 궤적을 변경해야 하는지를 판단할 수 있다.

점진적 열 성능 저하(Graceful Thermal Degradation)를 적용하면 과열이 즉시 비행 필수 고장으로 전환되는 것을 방지할 수 있다. 고성능 컴퓨터는 핵심 비행 제어 기능을 유지하면서 프로세서 또는 GPU 주파수를 낮추거나, 비필수 연산을 중지하거나, 센서 처리 주기를 낮추거나, 선택적인 인공지능 기능을 중단할 수 있다. 비필수 임무 장비도 정지시킬 수 있다. 따라서 열 관리는 안전 비행에 필요한 최소 기능을 보호하기 위해 연산 스케줄링 및 전기적 부하 차단(Load Shedding)과 상호작용한다.

비행 필수 연산(Flight-Critical Computing)과 임무 필수 연산(Mission-Critical Computing)의 구분은 냉각 자원 할당에서 중요하다. FCC 기능은 예측 가능한 가용성이 필요하며 안전 역할에 적합한 냉각 자원을 우선적으로 제공받아야 한다. 상위 수준의 AI 인지, 임무 최적화, 탑재체 처리, 데이터 기록은 훨씬 많은 전력을 소비할 수 있지만 통제된 성능 감소를 허용할 수 있는 경우가 많다. 따라서 열적 우선순위는 단순히 각 장비의 발열량이 아니라 기능 중요도(Functional Criticality)를 반영해야 한다.

항공전자 전원 아키텍처(Avionics Power Architecture)와 냉각 아키텍처(Cooling Architecture)는 강하게 결합되어 있다. 전력 변환 손실은 열 부하가 되며, 팬, 펌프, 밸브, 냉각 제어기 자체도 전력을 소비한다. 따라서 전기 시스템의 성능이 저하되면 남아 있는 변환기가 더 높은 부하를 담당하는 바로 그 시점에 냉각 능력까지 감소할 수 있다. 현실적인 고장 조건을 평가하고 각 아키텍처가 독립적으로 무제한의 지원 자원을 가진다는 잘못된 가정을 피하기 위해 전기-열 통합 해석(Joint Electrical-Thermal Analysis)이 필요하다.

환경 조건(Environmental Condition)은 추가적인 설계 제약을 발생시킨다. 화물 무인항공기의 항공전자 장비는 높은 온도와 낮은 온도, 태양 복사열(Solar Heating), 습도, 비, 먼지, 염분 오염, 고도에 따른 압력 변화, 급격한 열적 천이에 노출될 수 있다. 밀폐형 인클로저는 환경 보호 능력을 높이지만 대류를 제한하고, 환기형 시스템은 공기 흐름을 개선하지만 오염에 대한 노출을 증가시킨다. 따라서 냉각 설계에서는 환경 밀폐, 열 방출, 정비성, 질량, 신뢰성 사이의 균형을 고려해야 한다.

고도(Altitude)는 공기 밀도 감소를 통해 대류 열전달 성능에 영향을 주기 때문에 공랭 성능에도 영향을 준다. 지상 시험에서 충분한 성능을 보이는 냉각 시스템이라도 운용 고도에서는 열적 여유가 감소할 수 있으며, 특히 상승 또는 순항 중에도 높은 연산 부하가 지속된다면 더욱 중요하다. 따라서 팬과 열교환기는 대표적인 대기 조건에서 평가해야 하며, 열 모델에는 공기 밀도, 온도, 압력, 항공기 운용 상태의 변화를 반영해야 한다.

전자기 적합성(Electromagnetic Compatibility, EMC) 역시 냉각 설계와 상호작용한다. 대형 환기구는 인클로저의 차폐 성능을 약화시킬 수 있으며, 팬과 펌프 및 이들의 전자 구동장치는 전기적 노이즈를 발생시킬 수 있다. 전도성 열전달 경로가 동시에 접지 또는 본딩(Bonding) 경로가 될 수도 있다. 따라서 냉각 인터페이스는 인클로저 설계, 차폐, 접지, 필터링, 케이블 라우팅과 조정하여 열 성능 개선이 새로운 전자기 간섭이나 전기 안전 문제를 발생시키지 않도록 해야 한다.

열 해석(Thermal Analysis)은 해석적 계산, 시뮬레이션, 부품 특성 평가, 물리적 시험을 결합해야 한다. 초기 모델은 실제 하드웨어가 존재하기 전에 열전달 경로와 장비 온도를 추정할 수 있으며, 상세 전산 해석은 국부적인 공기 흐름이나 전도 문제를 식별할 수 있다. 이후 통제된 환경 조건에서 시제품 시험(Prototype Testing)을 수행하여 설계 가정을 검증하고 모델을 상관 분석하며 대표적인 부하 및 고장 조건에서 충분한 열적 여유가 유지되는지를 확인해야 한다.

검증(Verification)은 정상 냉각 상태만 입증하는 것이 아니라 비정상 조건도 포함해야 한다. 관련성이 있는 경우 팬 고장, 펌프 성능 저하, 공기 흐름 차단, 프로세서 부하 증가, 높은 주변 온도, 부분적인 전원 시스템 고장, 센서 고장, 열전달 인터페이스 성능 저하를 고려해야 한다. 목적은 온도가 얼마나 빠르게 상승하고 어떤 기능이 영향을 받으며 감시 시스템이 이를 탐지할 수 있는지, 그리고 필수 항공전자 기능이 얼마나 오랫동안 운용 가능한지를 판단하는 것이다.

정비 전략(Maintenance Strategy)은 항공기 전체 수명주기 동안 냉각 성능을 유지할 수 있어야 한다. 팬, 필터, 펌프, 냉각수, 열 인터페이스 재료, 열교환기, 환기 통로는 점진적으로 성능이 저하될 수 있다. 온도 변화 추세와 냉각 시스템 상태 기록을 이용하면 운용 한계를 초과하기 전에 열저항 증가 또는 공기 흐름 감소를 식별하는 예측 정비(Predictive Maintenance)가 가능하다. 장비 접근성을 높이는 배치 역시 검사와 교체의 비용 및 위험을 줄여준다.

화물 무인항공기가 2.5톤급에서 5톤급, 10톤급으로 발전함에 따라 항공전자 냉각은 차량 수준 열 관리(Vehicle-Level Thermal Management)와 더욱 긴밀하게 통합된다. 대형 항공기에는 더욱 강력한 컴퓨터, 중복 전자장치, 통신 시스템, 하이브리드 전원 제어기, 자율 연산 하드웨어를 탑재할 수 있다. 따라서 미래 설계에서는 하나의 범용 냉각 방식에 의존하기보다 분산 전도 냉각, 강제 공랭, 액체 냉각, 중앙집중식 열 방출(Centralized Heat Rejection)을 결합할 수 있다.

Volume 18에서 항공전자 냉각 설계(Avionics Cooling Design)는 FCC/FMC 아키텍처(FCC/FMC Architecture), 중복 항공전자 설계(Redundant Avionics Design), DO-254 하드웨어 설계(DO-254 Hardware Design), 항공전자 전원 아키텍처(Avionics Power Architecture)에 이어 항공전자 아키텍처(Avionics Architecture) 장을 완성한다. 이후 장에서는 항공우주 프로토콜(Aerospace Protocol)과 비행 제어 시스템(Flight-Control System)을 다루고, 후반부에서는 하이브리드 전원과 단계적으로 대형화되는 화물 무인항공기 플랫폼을 다룬다. 이러한 구조는 냉각이 신뢰할 수 있는 연산, 중복성, 통신, 제어 및 안전한 자율 비행을 가능하게 하는 핵심 기반 계층임을 보여준다.
