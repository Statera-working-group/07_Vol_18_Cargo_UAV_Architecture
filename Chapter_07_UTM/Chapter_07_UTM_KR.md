**Volume 18. Cargo UAV Architecture**

# Chapter 07. UTM

## 07.01. U-Space Architecture

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

유스페이스(U-Space)는 공유 공역(Shared Airspace)에서 무인항공기(Unmanned Aircraft)의 안전하고 확장 가능하며 고도로 자동화된 운용을 지원하기 위한 디지털 공역 관리 구조(Digital Airspace Management Architecture)이다. 화물 무인항공기(Cargo UAV) 환경에서는 항공기 운용자(Aircraft Operator), 서비스 제공자(Service Provider), 항공교통 당국(Air Traffic Authority), 인프라 운영자(Infrastructure Operator), 기타 공역 사용자 사이의 조정 계층(Coordination Layer)을 제공한다. 유스페이스는 단일 중앙집중형 제어 시스템(Centralized Control System)이 아니라 운용 정보를 지속적으로 교환하는 상호 연결된 디지털 서비스 생태계(Digital Service Ecosystem)로 구성된다.

이 구조는 기체 탑재 비행제어(Onboard Flight Control)와 외부 교통 및 공역 조정(External Traffic and Airspace Coordination)을 분리한다. 비행제어컴퓨터(Flight Control Computer, FCC)와 자동조종장치(Autopilot)는 항공기의 즉각적인 안정화, 항법, 유도 및 안전 필수 대응을 담당하고, 유스페이스(U-Space)는 비행 승인(Flight Authorization), 공역 제약조건(Airspace Constraints), 교통 상황(Traffic Conditions), 경로 충돌(Route Conflicts), 운용 제한(Operational Restrictions)과 같은 전략적 정보를 관리한다. 이러한 분리는 외부 네트워크 서비스가 항공기의 기본 안정화 제어 루프(Stabilization Control Loop)에 직접 포함되는 것을 방지하면서 네트워크 수준의 운항 조정을 가능하게 한다.

일반적인 유스페이스(U-Space) 환경에는 무인항공기 운용자(UAV Operator), 유스페이스 서비스 제공자(U-Space Service Provider), 공통정보서비스(Common Information Services), 항행 관련 기관(Air Navigation Organization), 규제기관(Regulatory Authority), 지원 인프라(Supporting Infrastructure)가 포함된다. 공통정보 기능은 공역 구조(Airspace Structure), 운용 제한, 기상 정보(Weather Information), 항공정보(Aeronautical Data), 관련 교통 정보(Traffic Information)와 같은 권위 있는 데이터를 배포한다. 서비스 제공자는 이러한 공유 자원과 항공기 및 임무 정보를 결합하여 개별 무인항공기 운용자와 기단관리시스템(Fleet Management System)에 운용 서비스를 제공한다.

출발 전 화물 무인항공기(Cargo UAV)의 임무계획시스템(Mission Planning System)은 출발지, 목적지, 항공기 성능, 탑재화물(Payload), 가용 에너지, 기상 및 운용 제약조건을 이용하여 비행 예정 경로를 생성한다. 이 경로는 유스페이스 서비스 환경을 통해 제출되며 관제 공역(Controlled Airspace), 제한 구역(Restricted Areas), 임시 제한사항(Temporary Limitations), 지오펜싱 경계(Geofencing Boundaries), 다른 계획 운항과의 관계를 검증한다. 최종 운항 승인(Operational Authorization)은 단순한 정적 비행계획이 아니라 지상통제국(Ground Control Station, GCS)과 임무관리시스템(Mission Management System)이 준수해야 하는 운용 제약조건으로 사용된다.

비행 중 항공기는 디지털 운항 식별정보(Digital Operational Identity)를 유지하고 위치, 고도, 속도, 궤적(Trajectory), 운항 상태 및 기타 필요한 정보를 주기적으로 전달한다. 이러한 데이터를 이용하여 유스페이스 서비스는 지속적으로 갱신되는 교통 상황도(Traffic Picture)를 구성한다. 이에 따라 다른 참여 항공기를 전략적 및 전술적 수준에서 모두 고려할 수 있다. 또한 일시적인 통신 단절이 발생하더라도 네트워크 연결 손실 자체가 즉각적으로 항공기의 불안전 상태를 초래하지 않도록 구조를 설계해야 한다.

교통관리(Traffic Management)는 여러 시간 범위(Time Horizon)에 걸쳐 수행된다. 전략적 충돌관리(Strategic Conflict Management)는 비행 전에 예정된 궤적을 평가하여 서로 양립할 수 없는 운항이 동시에 승인되는 것을 방지한다. 동적 관리(Dynamic Management)는 상황 변화에 따라 제한사항과 교통 정보를 갱신한다. 전술적 기능(Tactical Function)은 실제 비행궤적이 계획에서 벗어나거나 예상하지 못한 항공기가 운항 영역에 진입했을 때 대응을 지원한다. 즉각적인 분리 기동(Separation Maneuver)이 필요한 경우에는 기체 탑재 충돌회피시스템(Onboard Collision Avoidance System)이 독립적인 최종 안전 계층(Final Safety Layer)으로 기능한다.

지상통제국(Ground Control Station, GCS)은 화물 무인항공기와 유스페이스 생태계 사이의 핵심 운용 인터페이스(Operational Interface)를 제공한다. 임무 승인(Mission Authorization), 경로 갱신(Route Update), 지오펜스 변경(Geofence Change), 교통 주의정보(Traffic Advisory), 기상 경고(Weather Warning), 비상대응 정보(Contingency Information)를 GCS 통신 구조를 통해 수신할 수 있다. 반대 방향으로는 항공기 위치, 임무 상태, 시스템 건전성(System Health), 비상 상태(Contingency State), 운항 의도(Operational Intent)를 외부 서비스에 제공할 수 있다. 이러한 인터페이스는 직접적인 안전 필수 비행제어 채널(Safety-Critical Flight-Control Channel)과 논리적으로 분리되어야 한다.

화물 무인항공기 운용은 항공기 질량, 운동에너지(Kinetic Energy), 운항 거리 및 사고 결과의 심각성이 크게 증가하기 때문에 소형 배송 드론보다 높은 수준의 요구사항을 가진다. 2.5톤, 5톤 또는 향후 10톤급 화물 플랫폼은 물류 허브(Logistics Hub), 항만, 공항, 산업단지 및 지역 물류센터 사이를 운항할 수 있다. 따라서 유스페이스(U-Space)는 비행 승인, 화물 일정(Cargo Schedule), 버티포트(Vertiport) 가용성, 충전 또는 연료보급, 정비 상태(Maintenance Status), 기단 배차(Fleet Dispatch)를 궁극적으로 통합 조정하는 대규모 물류 인프라의 일부가 된다.

지오펜싱(Geofencing)은 유스페이스 정보를 기체 탑재 자율비행(Onboard Autonomy)과 연결하는 주요 실행 메커니즘 중 하나이다. 정적 경계(Static Boundary)는 영구적인 비행금지 또는 통제구역을 나타낼 수 있으며, 동적 지오펜스(Dynamic Geofence)는 임시 제한구역, 긴급사고 현장, 위험 기상, 인프라 사고 또는 특수 작전지역을 표현할 수 있다. 갱신된 경계정보는 임무시스템(Mission System)으로 전달되어 계획된 비행궤적과 실제 비행궤적을 비교하는 데 사용된다. 항공기는 최후 순간의 비행영역 제한에만 의존하지 않고 사전에 경로 재설정(Rerouting)을 수행할 수 있도록 지오펜스 위반 가능성을 충분히 일찍 감지해야 한다.

유스페이스(U-Space)는 공중 시스템과 지상 시스템 사이의 신뢰성 높은 정보교환에 의존하기 때문에 통신 구조(Communication Architecture)가 매우 중요하다. 명령 및 제어(Command and Control), 원격측정(Telemetry), 식별정보(Identification), 교통 정보 및 고대역폭 임무 데이터(High-Bandwidth Mission Data)를 위해 서로 다른 통신 링크를 사용할 수 있다. 셀룰러 네트워크(Cellular Network), 전용 항공통신 링크(Dedicated Aviation Link), 위성통신(Satellite Communication), 지역 인프라 통신(Local Infrastructure)이 이기종 통신 구조(Heterogeneous Communication Architecture)에서 공존할 수 있다. 장거리 화물 무인항공기의 경우 운항 지역에 따라 통신 가용성이 크게 달라질 수 있으므로 이중화 통신 경로(Redundant Communication Path)가 특히 중요하다.

사이버보안(Cybersecurity)은 배치 이후 추가되는 기능이 아니라 초기 시스템 구조 단계부터 포함되어야 한다. 항공기 식별정보(Aircraft Identity), 운용자 식별정보(Operator Identity), 승인 메시지(Authorization Message), 궤적 정보교환(Trajectory Exchange), 지오펜스 갱신, 명령 관련 정보에는 인증(Authentication), 무결성 보호(Integrity Protection), 접근통제(Access Control), 추적성(Traceability)이 필요하다. 유스페이스 정보가 침해되면 잘못된 경로 설정이나 허위 운항 제한이 발생할 수 있다. 따라서 보안 모니터링(Security Monitoring), 자격증명 관리(Credential Management), 보안 통신(Secure Communication), 로그 기록(Logging), 통제된 소프트웨어 업데이트(Controlled Software Update)가 전체 운용 신뢰 구조(Operational Trust Architecture)의 일부를 구성해야 한다.

비상상황 관리(Contingency Management)는 유스페이스와 항공기의 페일세이프 구조(Failsafe Architecture)를 연결한다. 명령 링크 손실(Loss of Command Link), GNSS 성능 저하, 추진계 이상(Propulsion Anomaly), 에너지 예비량 부족, 악천후, 항법 불확실성(Navigation Uncertainty), 비상착륙 요구 등이 승인된 비행궤적에서 벗어나야 하는 원인이 될 수 있다. 항공기와 GCS는 비상상황을 분류하고 적절한 대응을 선택하며 통신이 가능한 경우 변경된 운항 의도(Operational Intent)를 전달해야 한다. 외부 교통 서비스는 이를 이용해 주변 운용자에게 경고하고 해당 항공기 주변의 안전 분리(Separation)를 유지하도록 지원할 수 있다.

화물 무인항공기의 비행경로가 관제 공역 또는 유·무인 혼합 공역(Mixed-Use Airspace)을 통과하는 경우 유스페이스는 기존 항공교통관리(Air Traffic Management, ATM)와도 연계되어야 한다. UTM 방식의 자동화 서비스와 전통적인 ATM 사이의 경계를 단순히 독립된 게이트웨이(Gateway)로 취급할 수 없는 이유는 대형 화물 무인항공기가 하나의 임무 중 두 환경을 모두 통과할 수 있기 때문이다. 따라서 정보교환 구조는 기존 항공 시스템의 권한과 안전 책임을 유지하면서 공역 상태, 비행 의도, 식별정보, 교통 상황인식(Traffic Awareness), 전환 절차(Transition Procedure)를 조정할 수 있어야 한다.

운용이 단일 항공기에서 기단(Fleet)으로 확대될수록 확장성(Scalability)은 더욱 중요해진다. 기단관리시스템(Fleet Management System)은 수십 대에서 궁극적으로 수백 대의 화물 무인항공기 임무를 동시에 감독할 수 있으며, 유스페이스는 동일한 공역을 사용하는 다른 운용자의 항공기까지 함께 조정해야 한다. 따라서 자동 운항 승인(Automated Authorization), 궤적 협상(Trajectory Negotiation), 충돌 탐지(Conflict Detection), 동적 경로 재설정(Dynamic Rerouting), 기단 우선순위 관리(Fleet Prioritization), 예외상황 처리(Exception Handling)가 핵심 기능이 된다. 인간 운용자는 모든 일상 비행을 직접 조정하기보다 비정상 상황과 감독 수준의 의사결정에 집중해야 한다.

최종적인 유스페이스 구조는 기체 탑재 항공전자시스템(Onboard Avionics)에서 지역 공역 인프라(Regional Airspace Infrastructure)까지 확장되는 계층형 운용 시스템(Layered Operational System)으로 이해할 수 있다. 비행제어(Flight Control)는 항공기 안정성과 즉각적인 안전을 유지하고, 임무관리(Mission Management)는 승인된 궤적을 실행하며, GCS는 항공기를 감독한다. 기단 시스템(Fleet System)은 다수 항공기를 조정하고, 유스페이스 서비스는 공유 저고도 공역의 운항을 조정하며, ATM 인터페이스는 이러한 운항을 더 넓은 항공교통 체계와 연결한다. 각 계층은 정보를 교환하면서도 명확하게 정의된 책임과 고장 경계(Failure Boundary)를 유지한다.

대형 화물 무인항공기 개발에서 유스페이스(U-Space)는 단순한 외부 규제 서비스가 아니라 항공기의 시스템 오브 시스템즈 구조(System-of-Systems Architecture)의 일부로 다루어져야 한다. 항공전자시스템(Avionics), 데이터링크(Datalink), GCS, 기단관리(Fleet Management), 지오펜싱, 충돌회피(Collision Avoidance), 사이버보안, 물류 인프라 및 규제 준수(Regulatory Compliance)는 상호 호환되는 운용 인터페이스를 중심으로 통합 설계되어야 한다. 이러한 접근은 초기 2.5톤급 플랫폼에서 5톤 및 10톤급 화물 무인항공기 네트워크로 확장하면서도 통제 가능하고 추적 가능하며 점차 자동화되는 공역 통합(Airspace Integration)을 가능하게 한다.

## 07.02. UTM Protocol Design

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

무인교통관리(Unmanned Traffic Management, UTM) 프로토콜 설계(Protocol Design)는 무인항공기(UAV), 지상통제국(Ground Control Station, GCS), 기단 시스템(Fleet System), UTM 서비스 제공자(UTM Service Provider), 항공 당국(Aviation Authority)이 운항 정보를 일관되고 신뢰성 있게 교환하는 방법을 정의한다. 화물 무인항공기(Cargo UAV) 운항에서 프로토콜 계층(Protocol Layer)은 항공기 식별, 비행 의도, 운항 승인, 위치 보고, 교통 정보, 공역 제약, 비상상황 통보, 임무 갱신을 지원하면서 안전 필수 기체 탑재 비행제어 기능(Safety-Critical Onboard Flight-Control Function)과 명확하게 분리되어야 한다.

프로토콜 구조(Protocol Architecture)는 모든 참여자가 하나의 중앙 서버(Central Server)를 통해 통신한다고 가정하기보다 분산 서비스 지향 모델(Distributed Service-Oriented Model)을 따라야 한다. 무인항공기 운용자(UAV Operator)와 기단 시스템은 UTM 서비스 제공자와 상호작용하며, 권위 있는 공역, 규제, 기상 및 항공정보(Aeronautical Information)는 별도의 정보 서비스에서 제공될 수 있다. 표준화된 인터페이스(Standardized Interface)는 독립적으로 운영되는 시스템들이 동일한 내부 소프트웨어나 하드웨어 구조를 사용하지 않더라도 데이터를 교환할 수 있도록 한다.

항공기 식별(Aircraft Identification)은 기본적인 프로토콜 기능 중 하나를 구성한다. 참여하는 각 무인항공기는 운용자, 승인된 임무, 항공기 구성, 현재 운항 상태와 연계할 수 있는 고유한 운항 식별정보(Operational Identity)를 가져야 한다. 식별 메시지는 빈번한 전송이 가능하도록 충분히 간결하면서도 승인된 서비스가 어떤 항공기가 운항 중인지, 어떤 임무에 속하는지, 어떤 주체가 해당 운항에 책임을 지는지를 판단할 수 있는 충분한 정보를 제공해야 한다.

비행 의도 교환(Flight Intent Exchange)은 항공기가 시간에 따라 어디에서 운항할 계획인지를 표현한다. 임무를 단순히 지리적 웨이포인트(Geographic Waypoint)의 연속으로 표현하는 대신 UTM 프로토콜은 위치, 고도, 시간, 비행경로 회랑(Route Corridor), 운용 공간(Operational Volume), 불확실성 정보(Uncertainty Information)를 이용하여 예정 궤적(Intended Trajectory)을 표현할 수 있다. 이를 통해 교통관리 서비스는 여러 예정 운항을 비교하고 항공기가 실제로 서로 접근하기 전에 잠재적인 충돌을 식별할 수 있다.

비행 승인 프로토콜(Flight Authorization Protocol)은 임무계획(Mission Planning)을 통제된 공역 접근(Controlled Airspace Access)과 연결한다. GCS 또는 기단관리시스템(Fleet Management System)은 항공기 식별정보, 운용자 정보, 출발 및 목적 지역, 요청 시간대, 고도 범위, 비행경로, 관련 임무 제약조건을 포함하는 운항 계획을 제출한다. UTM 서비스는 요청을 평가하고 승인, 거부, 조건부 승인(Conditional Approval) 또는 수정 요구사항을 반환하며, 임무시스템(Mission System)은 이를 모호하지 않게 해석할 수 있어야 한다.

위치 보고(Position Reporting)는 출발 이후 교통 상황인식(Traffic Awareness)을 유지하는 데 필요한 동적 상태정보(Dynamic State Information)를 제공한다. 운용 요구조건에 따라 보고 데이터에는 위도, 경도, 고도, 지상속도(Ground Speed), 수직속도(Vertical Speed), 방위(Heading), 타임스탬프(Timestamp), 항법 품질(Navigation Quality), 운항 상태가 포함될 수 있다. 교통관리 결정은 항공기가 어디에 있다고 보고되었는지만이 아니라 해당 상태가 언제 측정되었고 위치 추정이 얼마나 신뢰할 수 있는지에도 의존하므로 메시지 타임스탬프는 특히 중요하다.

교통 정보 프로토콜(Traffic Information Protocol)은 주변 항공기와 운용 공간에 관한 관련 정보를 배포한다. 모든 알려진 항공기의 정보를 모든 무인항공기에 전송하는 것이 반드시 목적은 아니다. UTM 서비스는 지리적 영역, 고도, 궤적 관련성(Trajectory Relevance), 충돌 가능성(Conflict Probability)에 따라 정보를 필터링할 수 있다. 이를 통해 불필요한 통신 부하를 줄이면서 GCS, 임무 컴퓨터(Mission Computer), 적절한 기체 탑재 시스템이 현재 운항에 필요한 충분한 상황인식(Situational Awareness)을 유지할 수 있다.

지오펜싱 정보(Geofencing Information)를 처리하려면 정적 및 동적 공역 제약조건(Static and Dynamic Airspace Constraints)을 모두 표현할 수 있는 프로토콜이 필요하다. 제한사항에는 지리적 경계, 고도 제한, 활성화 및 종료 시간, 제한 유형, 관할기관 정보, 운용 조건이 포함될 수 있다. 동적 갱신(Dynamic Update)에는 버전 또는 유효성 정보(Validity Information)가 포함되어야 하며, 이를 통해 수신 시스템은 임무를 실행하거나 수정하기 전에 로컬에 저장된 지오펜스 데이터베이스(Geofence Database)가 최신 상태인지 판단할 수 있다.

프로토콜 설계는 전략적 충돌관리(Strategic Conflict Management)와 전술적 충돌회피(Tactical Collision Avoidance)를 구분해야 한다. 전략적 UTM 메시지는 즉각적인 충돌 위험이 발생하기 전에 궤적 조정, 운용 공간 협상(Operational-Volume Negotiation), 경로 재설정(Rerouting)을 지원한다. 전술적 충돌회피는 훨씬 짧은 시간 범위에서 작동하며 원격 네트워크 서비스에만 의존해서는 안 된다. 따라서 화물 무인항공기는 UTM 연결이 저하되거나 사용할 수 없는 경우에도 작동하는 기체 탑재 탐지 및 회피 기능(Onboard Detect-and-Avoid Capability)을 갖추어야 한다.

GCS와 UTM 서비스 사이의 통신은 명확하게 정의된 메시지 상태(Message State)와 트랜잭션 순서(Transaction Sequence)를 사용해야 한다. 예를 들어 비행 요청(Flight Request)은 제출, 검증, 승인, 활성화, 수정, 완료 또는 취소 상태를 거친다. 명시적인 상태 전환(State Transition)은 서로 다른 시스템이 동일한 임무를 다르게 해석하는 것을 방지하고 운용자, 서비스 제공자 또는 공역 당국에 의해 운항이 수정되었을 때 추적성(Traceability)을 제공한다.

비동기 이벤트 메시지(Asynchronous Event Message) 역시 중요하다. 많은 운항 변화는 주기적인 폴링(Periodic Polling)을 기다릴 수 없기 때문이다. 임시 비행 제한(Temporary Flight Restriction), 악천후 경고, 교통 충돌, 긴급 운항, 지오펜스 변경, 버티포트 폐쇄(Vertiport Closure), 운항 승인 변경은 즉시 전달되어야 할 수 있다. 따라서 발행-구독(Publish-Subscribe) 또는 이벤트 기반 통신(Event-Driven Communication) 메커니즘은 요청-응답 인터페이스(Request-Response Interface)를 보완하여 구독 시스템이 관련 변경사항을 발생 즉시 수신하도록 할 수 있다.

화물 무인항공기 프로토콜은 비상상황을 프로토콜 외부의 예외적인 데이터로 취급하지 않고 비상상황 통신(Contingency Communication)을 정상적인 구조 기능으로 지원해야 한다. 명령 링크 손실(Loss of Command Link), GNSS 성능 저하, 추진계 고장(Propulsion Fault), 에너지 부족, 예상하지 못한 우회(Diversion), 비상착륙, 승인된 비행궤적을 따를 수 없는 상황은 표준화된 비상상황 상태(Standardized Contingency State)로 표현되어야 한다. UTM 서비스는 이를 이용하여 영향을 받은 항공기의 상태와 수정된 운항 의도를 관련 공역 참여자에게 전달할 수 있다.

무선 및 광역 네트워크(Wide-Area Network)는 지속적인 연결성을 보장할 수 없기 때문에 신뢰성 메커니즘(Reliability Mechanism)이 필요하다. 메시지에는 순서번호(Sequence Number), 수신확인(Acknowledgement), 재전송 정책(Retransmission Policy), 만료시간(Expiration Time), 중복 탐지(Duplicate Detection), 로컬 버퍼링(Local Buffering)이 필요할 수 있다. 그러나 과도한 재전송은 성능이 저하된 네트워크에 부하를 줄 수 있으므로 프로토콜은 중요 운항 메시지와 낮은 우선순위 정보를 구분해야 한다. 또한 항공기 시스템은 UTM 정보를 갱신할 수 없는 기간 동안의 안전 동작(Safe Behavior)을 정의해야 한다.

시간 동기화(Time Synchronization)는 전체 UTM 생태계에서 필수적이다. 항공기 원격측정(Aircraft Telemetry), 궤적 예측(Trajectory Prediction), 승인 시간창(Authorization Window), 지오펜스 활성화, 충돌 계산, 이벤트 로그(Event Log)는 모두 일관된 타임스탬프에 의존한다. GNSS 기반 시간 또는 다른 동기화된 네트워크 시간원을 이용하여 공통 시간 기준(Common Temporal Reference)을 구축할 수 있다. 또한 부정확한 시간은 올바른 위치정보조차 잘못된 교통 데이터로 만들 수 있으므로 시스템은 타임스탬프 품질을 표시하고 비정상적인 시계 오프셋(Clock Offset)을 감지해야 한다.

사이버보안 요구사항(Cybersecurity Requirements)은 모든 프로토콜 인터페이스에 영향을 미친다. 인증(Authentication)은 항공기, 운용자, GCS 시스템, 서비스 제공자의 신원을 확인하며, 무결성 메커니즘(Integrity Mechanism)은 메시지가 승인 없이 변경되는 것을 방지한다. 암호화(Encryption)는 전송 중 민감한 운항 정보를 보호할 수 있으며, 권한부여 정책(Authorization Policy)은 각 참여자가 어떤 데이터에 접근하거나 수정할 수 있는지를 결정한다. 보안 자격증명(Security Credential)은 항공기 시운전, 운항, 정비, 소프트웨어 업데이트 및 최종 폐기 단계까지 전체 수명주기에 걸쳐 관리되어야 한다.

프로토콜 이중화(Protocol Redundancy)는 대형 화물 운항에서 단일 통신 의존성(Single Communication Dependency)이 발생하지 않도록 설계되어야 한다. 인구 밀집 지역에서는 셀룰러 네트워크가 주요 연결을 제공할 수 있고, 전용 항공통신 링크(Dedicated Aviation Link)는 명령 및 운항 데이터를 지원하며, 위성통신(Satellite Communication)은 원격 지역까지 통신 범위를 확장할 수 있다. 통신망이 전환되더라도 새로운 별개의 운항으로 인식되지 않도록 프로토콜은 네트워크 간에 일관된 항공기 식별정보, 임무 상태 및 메시지 의미(Message Semantics)를 유지해야 한다.

화물 무인항공기의 크기와 임무 범위가 증가할수록 기존 항공교통관리(Air Traffic Management, ATM)와의 상호운용성(Interoperability)이 더욱 중요해진다. 지역 화물 운송 임무는 UTM이 관리하는 저고도 환경과 기존 ATM 절차에 의해 관리되는 관제 공역 사이를 전환할 수 있다. 따라서 게이트웨이 인터페이스(Gateway Interface)는 운항 의미를 손실하거나 상충되는 권한 출처를 만들지 않으면서 비행 의도, 식별정보, 운항 승인, 교통 상태, 비상상황 정보를 변환하거나 연계해야 한다.

기단 규모 운용(Fleet-Scale Operation)은 하나의 운용자가 여러 항공기를 동시에 관리할 수 있기 때문에 또 다른 프로토콜 설계 차원을 추가한다. 기단관리시스템은 대량 임무 제출(Bulk Mission Submission), 항공기 상태 집계(Status Aggregation), 경로 수정, 우선순위 관리, 버티포트 일정관리(Vertiport Scheduling), 예외상황 처리를 위한 인터페이스가 필요하다. 프로토콜은 수백 개의 일상적인 상태 갱신 때문에 비정상 항공기 한 대와 관련된 긴급 메시지 처리가 지연되지 않도록 효율적인 그룹화(Grouping)와 필터링(Filtering)을 지원해야 한다.

데이터 모델(Data Model)은 화물 무인항공기 기술이 2.5톤급 플랫폼에서 5톤 및 10톤급 항공기로 발전하는 과정에서도 확장 가능해야 한다. 식별정보, 위치, 궤적, 운항 승인, 운항 상태와 같은 핵심 필드는 안정적으로 유지하고 선택적 확장(Optional Extension)을 통해 탑재화물 제한, 에너지 상태, 기체 성능, 기상 허용범위(Weather Tolerance), 버티포트 호환성(Vertiport Compatibility), 미래 자율 협조 기능(Autonomous Coordination Function)을 표현할 수 있다. 따라서 신형 시스템과 기존 시스템이 단계적인 배치 과정에서 공존할 수 있도록 버전 관리(Version Management)가 필요하다.

완전한 UTM 프로토콜 구조(UTM Protocol Archi

## 07.03. Geofencing System

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

지오펜싱(Geofencing)은 화물 무인항공기(Cargo UAV)가 운항할 수 있는 영역과 비행이 제한되거나 조건부로 허용되거나 금지되는 영역을 정의하는 디지털 공역 보호 메커니즘(Digital Airspace Protection Mechanism)이다. UTM 및 유스페이스(U-Space) 구조에서 지오펜싱 시스템은 규제, 운용, 안전 및 인프라 제약조건을 기계 판독 가능한 지리적 경계(Machine-Readable Geographic Boundary)로 변환한다. 이러한 경계는 임무계획, 지상통제국(Ground Control Station, GCS), 기단관리(Fleet Management), 기체 탑재 항법시스템(Onboard Navigation System)이 평가할 수 있는 능동적인 임무 제약조건으로 사용된다.

지오펜스(Geofence)는 지도에 표시된 단순한 2차원 다각형(Two-Dimensional Polygon) 이상의 개념이다. 자율 화물 무인항공기 운항에서는 일반적으로 위도, 경도, 고도 제한 및 적용 시간을 포함하는 3차원 또는 4차원 운용 제약조건(Three- or Four-Dimensional Operational Constraint)을 표현해야 한다. 이를 통해 동일한 지리적 영역에서도 고도나 시간에 따라 서로 다른 제한조건을 적용할 수 있다. 이러한 표현 방식은 도시 지역, 공항, 항만, 산업지역 및 관제 공역을 통과하는 지역 화물 운송 경로에서 특히 중요하다.

정적 지오펜스(Static Geofence)는 시간에 따라 비교적 안정적으로 유지되는 제한사항을 나타낸다. 비행금지 공역, 공항 보호구역, 군사시설, 핵심 인프라(Critical Infrastructure), 국경, 영구 장애물 지역 및 특별 승인이 필요한 장소 등이 이에 해당한다. 이러한 경계는 기체 탑재 또는 GCS 지오펜스 데이터베이스(Geofence Database)에 저장되고 통제된 형상관리(Configuration Management)를 통해 갱신될 수 있다. 각 데이터셋에는 출처, 버전, 유효기간, 좌표 기준(Coordinate Reference), 적용되는 운용 규칙이 포함되어야 한다.

동적 지오펜스(Dynamic Geofence)는 일시적이거나 빠르게 변화하는 제한사항을 나타낸다. 긴급대응 지역, 산불지역, 악천후 영역, 임시 비행 제한(Temporary Flight Restriction), 보안 이벤트, 사고 현장, 이동하는 위험 작업 또는 일시적으로 사용할 수 없는 버티포트(Vertiport) 등이 동적 경계를 생성할 수 있다. UTM 또는 유스페이스 서비스는 이러한 변경사항을 영향을 받는 운용자에게 전달하며, 수신 시스템은 현재 운항 중이거나 계획된 화물 무인항공기 임무가 새롭게 제한된 영역과 교차하는지 판단해야 한다.

지오펜싱 구조(Geofencing Architecture)는 금지구역(Prohibited Zone), 조건부 구역(Conditional Zone), 주의구역(Advisory Zone)을 구분해야 한다. 금지구역은 정의된 운항 조건에서 진입을 방지하고, 조건부 구역은 적절한 승인, 고도, 항공기 성능 또는 임무 우선순위를 충족하는 경우에만 진입을 허용할 수 있다. 주의구역은 운용자 또는 자율 시스템(Autonomy System)에 증가된 위험을 경고하면서 운항을 계속 허용할 수 있다. 이러한 분류를 통해 모든 공역 제약조건이 동일한 항공기 대응을 발생시키는 것을 방지할 수 있다.

임무계획(Mission Planning)은 첫 번째 주요 지오펜스 적용 단계(Enforcement Stage)이다. 출발 전에 계획된 비행궤적을 고도 및 시간 제약조건을 포함하는 활성 지오펜스 데이터베이스와 비교한다. 비행경로가 금지구역과 교차하면 임무계획 시스템은 해당 궤적을 거부하거나 새로운 경로를 생성해야 한다. 조건부 구역에서는 운항 승인 확인이 필요하며, 주의구역은 위험도 평가(Risk Evaluation)에 영향을 줄 수 있다. 이러한 전략적 검증은 항공기가 본질적으로 유효하지 않은 비행계획으로 임무를 시작할 가능성을 줄인다.

승인된 비행경로와 공역 조건은 비행 중에도 변경될 수 있으므로 지오펜스 감시(Geofence Monitoring)는 이륙 후에도 계속된다. 항공기 위치, 예측 비행궤적(Predicted Trajectory), 현재 지오펜스 집합을 지속적으로 비교하여 잠재적인 경계 위반을 식별한다. 감시 기능은 현재 항공기 위치뿐만 아니라 속도, 방위(Heading), 상승률(Climb Rate), 항법 불확실성(Navigation Uncertainty), 예상되는 미래 비행궤적까지 고려해야 한다. 조기 예측을 통해 경계 부근에서 급격한 기동을 수행하는 대신 충분한 시간을 확보하여 통제된 경로 재설정(Rerouting)을 수행할 수 있다.

실제 시스템에서는 중요한 경계 주변에 여러 단계의 보호 영역(Protection Region)을 사용하는 것이 바람직하다. 외부 인식 영역(Outer Awareness Region)은 항공기가 제한구역에 접근하고 있음을 임무시스템에 알릴 수 있으며, 경고 영역(Warning Region)은 경로 수정 또는 운용자의 주의 조치를 시작할 수 있다. 최종 격리 경계(Final Containment Boundary)는 위반이 임박한 경우 더욱 강력한 자율 대응을 활성화할 수 있다. 구체적인 대응 방식은 항공기 성능, 공역 요구조건, 기체 질량 및 경계 침범으로 발생할 수 있는 운용상의 결과에 따라 결정된다.

항법 불확실성(Navigation Uncertainty)은 지오펜스 계산에 포함되어야 한다. GNSS와 GNSS-RTK는 양호한 조건에서 높은 위치 정확도를 제공할 수 있지만 다중경로(Multipath), 전파 간섭(Interference), 재밍(Jamming), 대기 영향, 센서 고장 또는 위성 가시성 저하로 인해 위치 불확실성이 증가할 수 있다. 따라서 시스템은 보고된 위치를 수학적으로 정확한 하나의 점으로 간주해서는 안 된다. 항법 무결성(Navigation Integrity), 항공기 동역학(Aircraft Dynamics), 요구되는 격리 성능에 따라 제한 경계를 확장하는 안전여유(Safety Margin)를 적용할 수 있다.

기체 탑재 지오펜싱 기능(Onboard Geofencing Function)은 외부 통신이 일시적으로 손실된 경우에도 사용할 수 있어야 한다. 화물 무인항공기는 금지 공역에 진입하고 있는지를 판단하기 위해 지속적인 네트워크 연결에만 의존할 수 없다. 따라서 현재 유효한 지오펜스 데이터셋, 임무 승인(Mission Authorization), 핵심 경계 및 관련 대응 규칙을 기체 내부에서 사용할 수 있어야 한다. 네트워크 연결은 갱신정보를 수신하는 데 사용하며, 기체 탑재 로직(Onboard Logic)은 통신 성능이 저하되는 동안에도 기본적인 격리 기능(Containment Capability)을 유지한다.

UTM 및 유스페이스 인터페이스는 권위 있는 지오펜스 정보(Authoritative Geofence Information)를 배포하는 메커니즘을 제공한다. 갱신정보에는 경계 형상(Boundary Geometry), 고도 범위, 활성화 시간, 만료시간, 제한 유형, 발행기관, 우선순위 및 버전 정보가 포함될 수 있다. GCS 또는 기단 시스템은 메시지를 활성 운용 데이터베이스에 통합하기 전에 검증한다. 버전 관리(Version Control)는 오래된 제한사항이 새로운 정보를 의도치 않게 대체하는 것을 방지하고 비행 후 분석(Post-Flight Analysis)을 위한 추적성을 제공한다.

동적 지오펜스 갱신(Dynamic Geofence Update)에는 결정론적인 충돌 처리(Deterministic Conflict Handling)가 필요하다. 새로운 제한구역이 현재 운항 중인 비행경로를 직접 가로질러 이전에 승인된 비행궤적을 무효화할 수 있다. 시스템은 항공기가 경로를 재설정하거나, 대기(Hold)하거나, 복귀(Return)하거나, 대체 착륙장으로 우회(Divert)하거나, 기존 승인에 따라 계속 비행할 수 있는지를 판단해야 한다. 대형 화물 무인항공기는 속도, 관성, 에너지 상태, 착륙 요구조건 및 기동 한계로 인해 새롭게 설정된 경계를 즉각 준수하기 어려울 수 있으므로 특별한 고려가 필요하다.

지오펜싱은 탐지 및 회피(Detect-and-Avoid)와 충돌회피(Collision Avoidance) 기능과 긴밀하게 상호작용해야 하지만 이들을 대체해서는 안 된다. 지오펜싱은 주로 정의된 공역으로의 진입을 방지하는 반면, 탐지 및 회피는 다른 항공기와 같은 동적 충돌 위험(Dynamic Collision Hazard)에 대응한다. 지오펜스 규칙상 완전히 유효한 비행경로에서도 교통 충돌이 발생할 수 있다. 반대로 주변에 항공기가 전혀 없는 공역도 비행금지구역일 수 있다. 따라서 두 기능은 서로 독립적인 운항 안전 계층(Operational Safety Layer)을 제공한다.

비상상황(Contingency Condition)에서는 정상적인 지오펜스 동작에서 통제된 이탈이 필요할 수 있다. 추진계 성능 저하, 악천후, 항법 능력 상실, 에너지 부족, 의료 또는 공공안전 임무, 비상착륙 요구사항 등은 원래 승인된 비행 회랑(Authorized Corridor) 내부에 머무르는 것이 오히려 더 위험한 상황을 만들 수 있다. 시스템 구조는 예외적인 조치에 대한 명확한 권한을 유지하면서 비상상태를 선언하고 기록하며 전달하고 UTM 서비스와 조정하는 방법을 정의해야 한다.

지오펜스 데이터의 악의적인 변경은 항공기의 경로를 변경하거나 정상적인 운항을 차단하거나 의도적으로 무인항공기를 제한된 핵심 인프라 방향으로 유도할 수 있기 때문에 사이버보안(Cybersecurity)은 매우 중요하다. 따라서 지오펜스 메시지와 데이터베이스에는 인증된 출처(Authenticated Source), 무결성 검증(Integrity Verification), 보안 배포(Secure Distribution), 접근통제(Access Control), 감사 로그(Audit Logging)가 필요하다. 민감한 갱신정보에는 암호화(Encryption)가 추가로 필요할 수 있다. 항공기와 GCS는 유효하지 않거나 손상되거나 승인되지 않았거나 만료되었거나 일관성이 없는 지오펜스 정보를 자동으로 적용하지 않고 거부해야 한다.

기단 운용(Fleet Operation)에서는 하나의 지오펜스 갱신이 여러 항공기에 동시에 영향을 미칠 수 있기 때문에 추가적인 복잡성이 발생한다. 기단관리시스템(Fleet Management System)은 변경된 제한사항과 교차하는 모든 현재 및 계획된 임무를 식별하고 그 영향을 평가해야 한다. 일부 항공기는 경로를 변경해야 하고 다른 항공기는 출발을 지연해야 할 수 있으며 영향을 받지 않는 임무는 정상적으로 계속되어야 한다. 수십 또는 수백 대의 화물 무인항공기가 지역 물류 회랑(Regional Logistics Corridor)을 공유하는 경우 자동 영향 분석(Automated Impact Analysis)의 중요성이 더욱 커진다.

버티포트(Vertiport)와 물류 허브(Logistics Hub)는 도착 및 출발 운항을 체계화하기 위해 지역 지오펜스(Local Geofence)를 사용할 수도 있다. 보호된 접근 회랑(Protected Approach Corridor), 착륙구역, 지상 안전구역(Ground Safety Region), 장애물 지역, 충전시설, 화물 취급구역, 비상착륙구역을 운용 경계로 표현할 수 있다. 정비 또는 사고가 발생하는 동안에는 임시 제한을 통해 특정 착륙 패드(Pad)를 격리할 수 있다. 이를 통해 공역 수준의 지오펜싱과 자동화된 화물 운송 네트워크가 사용하는 물리적 인프라가 연결된다.

2.5톤, 5톤 및 미래의 10톤급 화물 무인항공기에서는 소형 드론을 위해 개발된 규칙을 단순히 적용하는 것이 아니라 항공기 성능을 반영하여 지오펜스 대응을 설계해야 한다. 높은 질량과 운동에너지(Kinetic Energy)는 감속, 선회, 대기, 우회 및 비상착륙에 필요한 거리를 증가시킨다. 따라서 경계 예측은 항공기별 비행영역(Flight Envelope)과 대응시간(Response Time)을 고려해야 한다. 지오펜스 안전여유는 속도, 고도, 기상, 탑재화물(Payload), 항법 품질 및 비상상태에 따라 적응적으로 변경될 수 있다.

로그 기록(Logging)과 추적성(Traceability)은 인증(Certification), 운항 모니터링 및 사고 조사에 필수적이다. 시스템은 지오펜스 데이터셋 버전, 수신된 갱신정보, 승인 상태, 항공기 위치, 예측된 경계 접근, 경고, 경로 재설정 결정, 운용자 조치 및 자율 대응을 기록해야 한다. 동기화된 타임스탬프(Synchronized Timestamp)를 이용하면 비행 후 이러한 이벤트를 재구성할 수 있으며 항공기와 지원 시스템이 적절한 시점에 올바른 제한사항을 적용했다는 증거를 제공할 수 있다.

완전한 지오펜싱 시스템(Geofencing System)은 권위 있는 공역 정보에서 시작하여 UTM 및 유스페이스 서비스를 거쳐 기단관리, GCS 임무계획, 기체 탑재 항법 및 자율 페일세이프 기능(Autonomous Failsafe Function)까지 확장된다. 정적 및 동적 경계, 예측 감시(Predictive Monitoring), 항법 불확실성, 사이버보안, 통신 이중화(Communication Redundancy), 비상상황 처리 및 추적성이 하나의 통합된 구조로 작동해야 한다. 이를 통해 지오펜싱은 단순한 지도상의 제한에서 자율 화물 무인항공기 운항을 위한 능동적인 공역 안전 메커니즘(Active Airspace Safety Mechanism)으로 발전한다.

화물 무인항공기 네트워크가 지역 단위에서 궁극적으로 장거리 무인 물류(Long-Range Unmanned Logistics)로 확장됨에 따라 지오펜싱은 디지털 공역 거버넌스(Digital Airspace Governance)와 물리적 항공기 자율성(Physical Aircraft Autonomy)을 연결하는 핵심 인터페이스가 된다. 그 목적은 단순히 경계 위반을 방지하는 것이 아니라 각 항공기가 자신의 임무를 규정하는 공간적, 수직적, 시간적 및 운용 조건을 정확히 이해하도록 하는 것이다. 견고한 지오펜싱 구조는 정상, 성능 저하 및 비상 조건에서 예측 가능한 항공기 동작을 유지하면서 확장 가능한 기단 운용을 가능하게 한다.

## 07.04. UAV Collision Avoidance

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

무인항공기 충돌회피(UAV Collision Avoidance)는 다른 항공기, 장애물, 지형 및 제한된 운용 공간(Restricted Operating Volume)과의 잠재적 충돌을 탐지하고 관련 충돌 위험을 평가하며 적절한 회피 대응을 생성하는 안전 구조(Safety Architecture)이다. 화물 무인항공기(Cargo UAV)의 경우 대형 항공기는 관성이 크고 기동에 필요한 거리가 길며 안전 분리(Safe Separation)가 상실될 경우의 결과가 더욱 심각하므로 전략적 및 전술적 시간 범위(Strategic and Tactical Time Scale) 모두에서 이 기능이 작동해야 한다.

충돌회피(Collision Avoidance)는 하나의 알고리즘에 의존하기보다 여러 개의 독립적인 안전 계층(Independent Safety Layer)으로 구성되어야 한다. UTM 및 유스페이스(U-Space) 서비스는 충돌이 즉각적인 위험으로 발전하기 전에 전략적인 교통 조정(Strategic Traffic Coordination)을 제공하며, 기체 탑재 탐지 및 회피 시스템(Onboard Detect-and-Avoid System)은 비행 중 주변 환경을 감시한다. 비행제어(Flight Control)는 회피 명령을 안전한 항공기 움직임으로 변환하는 최종 실행 계층을 제공한다. 이러한 계층형 구조는 하나의 정보원이 고장 나더라도 전체 보호 기능이 상실되는 것을 방지한다.

전략적 충돌회피(Strategic Conflict Avoidance)는 임무계획(Mission Planning) 단계에서 시작된다. 계획된 비행궤적을 알려진 교통 상황, 승인된 운용 공간, 지오펜스(Geofence), 고도 제한, 기상조건 및 예정된 공역 활동과 비교한다. 예측된 궤적이 요구되는 분리 기준(Separation Criteria)을 위반하면 UTM 또는 기단관리시스템(Fleet Management System)은 이륙 전에 출발시간, 고도, 경로, 속도 프로파일 또는 운용 공간을 수정할 수 있다. 전략적 충돌 해소(Strategic Deconfliction)는 이후 공격적인 전술 기동을 통해 해결해야 하는 상황의 발생을 줄인다.

전술적 충돌회피(Tactical Collision Avoidance)는 비행 중 작동하며 비행 전 조정만으로 완전히 해결할 수 없는 충돌에 대응한다. 주변의 협력 항공기(Cooperative Aircraft)는 네트워크 또는 항공 감시체계(Aviation Surveillance Mechanism)를 통해 식별정보, 위치, 속도 및 궤적 정보를 전송할 수 있다. 비협력 항공기(Non-Cooperative Aircraft), 조류, 구조물, 크레인, 지형 또는 예상하지 못한 물체는 기체 탑재 인지(Onboard Perception)를 통해 탐지해야 한다. 따라서 시스템은 외부 교통 정보와 로컬 센싱(Local Sensing)을 결합하여 충돌 위험에 대한 지속적으로 갱신되는 표현을 생성한다.

기체 탑재 센서 구조(Onboard Sensor Architecture)는 항공기 요구조건에 따라 레이더(Radar), 라이다(LiDAR), 전자광학 카메라(Electro-Optical Camera), 적외선 카메라(Infrared Camera), GNSS, 관성측정장치(Inertial Measurement Unit, IMU) 및 기타 항법 또는 감시 센서를 조합할 수 있다. 각 센서는 탐지거리, 시야각(Field of View), 기상 대응성, 각도 분해능(Angular Resolution), 객체 분류 측면에서 서로 다른 장점을 제공한다. 센서 융합(Sensor Fusion)은 이러한 상호보완적 측정값을 결합하여 특정 환경조건에서 성능이 저하될 수 있는 단일 센싱 기술에 충돌회피 기능이 의존하지 않도록 한다.

객체 탐지(Object Detection)만으로는 충분하지 않다. 항공기는 탐지된 물체가 실제로 충돌 위협을 나타내는지를 판단해야 하기 때문이다. 추적 알고리즘(Tracking Algorithm)은 시간에 따른 주변 교통의 위치, 속도, 방위 및 불확실성을 추정한다. 이후 시스템은 상대운동(Relative Motion)을 예측하고 최근접 접근점(Closest Point of Approach), 최근접 접근시간(Time to Closest Approach), 분리거리(Separation Distance), 충돌확률(Collision Probability)과 같은 변수를 평가한다. 이러한 예측은 원시 인지 데이터(Raw Perception Data)를 회피 의사결정에 적합한 정보로 변환한다.

궤적 예측(Trajectory Prediction)은 화물 무인항공기와 주변 객체 모두의 불확실성을 고려해야 한다. 센서 잡음, 통신 지연, 항법 오차, 알 수 없는 조종 의도, 바람 및 기동 행동으로 인해 미래 위치가 불확실해질 수 있다. 회피 시스템은 하나의 결정론적 궤적(Deterministic Trajectory)을 가정하는 대신 불확실성 영역(Uncertainty Region) 또는 확률적 추정(Probabilistic Estimate)을 이용하여 예상 움직임을 표현할 수 있다. 교통 상태에 대한 신뢰도가 감소하면 안전여유(Safety Margin)를 증가시켜야 한다.

충돌 탐지(Conflict Detection)는 예측된 분리거리가 허용 가능한 임계값 이하로 감소하는 시점을 결정한다. 항공기 유형, 상대속도, 운용환경, 항법 품질 및 규제 요구조건에 따라 서로 다른 임계값을 적용할 수 있다. 고립된 물류 회랑(Logistics Corridor)에서 저속으로 이동하는 무인항공기는 관제 공역에 접근하는 고속 화물 항공기와 다른 보호 공간(Protection Volume)을 필요로 할 수 있다. 대형 화물 무인항공기는 소형 멀티로터 드론과 동일한 기동 응답을 수행할 수 있다고 가정할 수 없으므로 일반적으로 더 이른 충돌 탐지가 필요하다.

회피계획(Avoidance Planning)은 중요한 충돌이 식별된 후 항공기가 비행궤적을 어떻게 수정해야 하는지를 결정한다. 가능한 대응에는 수평 선회, 고도 변경, 속도 조정, 대기(Holding), 경로 이탈(Route Deviation) 또는 이러한 기동의 조합이 포함될 수 있다. 선택된 해결책은 즉각적인 위협을 회피하면서 2차 충돌(Secondary Conflict)을 발생시키거나 비행금지 공역에 진입하거나 비행영역(Flight Envelope)을 초과하거나 지형 안전고도(Terrain Clearance)를 위반하거나 남은 에너지를 허용할 수 없는 수준으로 소비해서는 안 된다.

따라서 회피계획기는 지오펜싱(Geofencing) 및 임무관리(Mission Management)와 상호작용해야 한다. 기하학적으로 단순한 회피 기동이라도 공항 보호구역, 제한구역, 지형 경계 또는 임시 비상 지오펜스(Emergency Geofence)를 통과한다면 유효하지 않을 수 있다. 반대로 다른 항공기가 예상하지 못하게 비행 회랑에 진입하면 원래 임무 경로를 엄격하게 유지하는 것이 위험할 수 있다. 일반적으로 충돌 안전(Collision Safety)이 즉각적으로 더 높은 우선순위를 가지며, 이후 시스템은 발생한 경로 이탈을 UTM 및 지상통제국(Ground Control Station, GCS)과 조정한다.

비행제어컴퓨터(Flight Control Computer, FCC)와의 통합은 회피 궤적을 실제 실행 가능한 유도 및 제어 명령(Guidance and Control Command)으로 변환하기 위해 필요하다. 회피계획기는 항공기별 뱅크각(Bank Angle), 상승률, 가속도, 대기속도(Airspeed), 추진 능력 및 구조 하중(Structural Loading) 한계를 준수하는 명령을 제공해야 한다. 대형 화물 무인항공기에서는 회피기동을 기체 동역학(Vehicle Dynamics)과 독립적으로 설계할 수 없다. 소형 드론에서 가능한 기동이 수 톤급 항공기에서는 물리적으로 불가능하거나 운용상 위험할 수 있다.

회피 동작은 단계적으로 강화되는 보호 단계(Escalating Protection Stage)를 따라야 한다. 장거리에서는 시스템이 감시 수준을 높이거나 전략적인 경로 재설정(Rerouting)을 요청할 수 있다. 예측된 충돌 위험이 증가하면 경고(Advisory)를 생성하고 대체 비행궤적을 준비할 수 있다. 정상적인 조정을 통해 필요한 분리거리를 더 이상 유지할 수 없으면 자율 회피(Autonomous Avoidance)가 필요할 수 있다. 이러한 단계적 접근은 불필요하게 공격적인 기동을 방지하면서 사용 가능한 의사결정 시간이 짧아지는 경우 신속한 대응 능력을 유지한다.

GCS와의 통신은 감독 수준의 상황인식(Supervisory Awareness)을 지원하지만 인간의 반응시간에 과도하게 의존해서는 안 된다. GCS는 충돌 가능성이 있는 교통, 예측된 조우 형상(Encounter Geometry), 회피 상태, 경로 변경 및 시스템 신뢰도를 표시할 수 있다. 충분한 시간이 있는 경우 운용자가 전략적 의사결정에 참여할 수 있지만, 충돌이 임박한 경우에는 네트워크 지연, 통신 손실 또는 인간의 대응 지연으로 적시에 개입하지 못할 수 있으므로 기체 탑재 자율 대응(Onboard Autonomous Action)이 필요하다.

UTM 및 유스페이스 서비스는 교통 정보를 배포하고 운항 의도(Operational Intent)를 조정함으로써 기체 탑재 충돌회피 기능을 보완한다. 회피기동으로 승인된 비행궤적이 변경된 후에는 통신이 가능한 경우 항공기 또는 GCS가 변경된 상태를 전달해야 한다. 교통 서비스는 주변 참여자의 정보를 갱신하고 새로운 비행궤적이 추가적인 충돌을 발생시키는지를 평가할 수 있다. 이를 통해 로컬 자율 안전(Local Autonomous Safety)과 네트워크 수준의 교통 조정(Network-Level Traffic Coordination) 사이에 피드백 루프(Feedback Loop)가 형성된다.

통신 손실(Loss of Communication)이 기본적인 충돌회피 기능을 무력화해서는 안 된다. 외부 교통 서비스를 사용할 수 없게 되더라도 항공기는 로컬 센싱, 추적, 위협 평가(Threat Assessment), 회피계획 및 비행제어 실행 기능을 유지해야 한다. 네트워크 정보가 없으면 상황인식 수준이 감소할 수 있으므로 더 큰 안전여유, 속도 감소, 경로 변경, 대기 또는 기타 성능 저하 모드(Degraded-Mode Behavior)가 필요할 수 있다. 시스템 구조는 연결 손실을 정의되지 않은 고장으로 취급하는 대신 이러한 전환을 명확하게 정의해야 한다.

센서 성능 저하(Sensor Degradation)에도 고장허용 동작(Fault-Tolerant Behavior)이 필요하다. 레이더는 전파 간섭을 받을 수 있고, 카메라는 어둠이나 눈부심의 영향을 받을 수 있으며, 라이다는 강수 조건에서 성능이 저하될 수 있고, GNSS는 전파 간섭이나 재밍의 영향을 받을 수 있다. 건전성 모니터링(Health Monitoring)은 센서 가용성과 측정 품질을 지속적으로 평가해야 한다. 하나의 정보원이 신뢰할 수 없게 되면 융합 알고리즘은 해당 센서의 영향력을 줄이고 나머지 정보원에 더 크게 의존하면서 불확실성을 증가시키고 운용 한계를 조정할 수 있다.

충돌회피 시스템은 공중 교통(Airborne Traffic)과 지형 및 고정 장애물(Fixed Obstacle)도 구분해야 한다. 건물, 타워, 크레인, 산악지형, 전력 인프라 및 버티포트 구조물은 이동 항공기처럼 움직이지 않지만 사용할 수 있는 회피 궤적을 제한할 수 있다. 지형 및 장애물 데이터베이스는 전략적 정보를 제공하고 기체 탑재 인지는 로컬 환경을 확인할 수 있다. 이러한 정보원을 결합하면 공중 충돌을 해결하는 과정에서 화물 무인항공기가 고정된 환경 위험요소를 향하도록 지시하는 상황을 방지할 수 있다.

기상(Weather)은 또 다른 동적 제약조건(Dynamic Constraint)을 제공한다. 강풍, 난기류, 강수, 결빙 또는 대류성 기상(Convective Weather)은 기동 성능과 센서 성능을 저하시키는 동시에 안전한 회피 방향을 제한할 수 있다. 따라서 충돌회피 시스템은 후보 비행궤적을 평가할 때 환경 상태를 고려해야 한다. 이론적으로 충돌이 없는 경로라도 바람으로 인해 항공기가 사용 가능한 시간 내에 필요한 선회, 상승 또는 측방 이동을 수행할 수 없다면 허용할 수 없다.

허위 교통 정보(False Traffic Information)가 의도적으로 불필요한 회피기동을 유발하거나 실제 충돌 위협을 은폐할 수 있으므로 사이버보안(Cybersecurity)이 중요하다. 따라서 협력 항공기의 교통 메시지는 인증(Authentication)되어야 하며 가능한 경우 사용 가능한 센서 관측정보와 일관성을 확인해야 한다. 시스템은 비현실적인 위치, 중복된 식별정보, 비정상적인 타임스탬프, 손상된 메시지 및 일관되지 않은 궤적을 탐지해야 한다. 검증되지 않은 하나의 네트워크 메시지만으로 안전 필수 항공기 움직임(Safety-Critical Aircraft Motion)을 자동으로 명령하도록 허용해서는 안 된다.

기단 규모의 화물 운항(Fleet-Scale Cargo Operation)에서는 다수 항공기에 대한 조정된 충돌관리(Coordinated Collision Management)가 필요하다. 기단 시스템은 출발 슬롯(Departure Slot)을 계획하고, 고도 계층(Altitude Layer)을 할당하고, 비행경로를 분리하며, 공유 물류 회랑을 관리하여 충돌 가능성을 줄일 수 있다. 그러나 예상하지 못한 교통과 비행경로 이탈을 일정관리만으로 완전히 제거할 수 없으므로 로컬 탐지 및 회피(Local Detect-and-Avoid)는 여전히 필요하다. 따라서 전략적 기단 조정과 전술적 기체 탑재 회피는 경쟁하는 제어 시스템이 아니라 상호보완적인 메커니즘으로 함께 작동한다.

중요한 모든 충돌회피 이벤트는 검증(Validation), 인증(Certification) 및 운용 개선을 위해 기록되어야 한다. 로그에는 센서 관측정보, 추적 객체, 예측 비행궤적, 불확실성 추정, 충돌 임계값, 선택된 회피 동작, 비행제어 응답, 운용자 상호작용 및 UTM 메시지가 포함되어야 한다. 정확한 시간 동기화(Time Synchronization)를 통해 전체 조우 상황을 재구성할 수 있으며 시스템이 요구되는 성능 범위 내에서 위험을 탐지하고 대응했는지를 검증할 수 있다.

2.5톤, 5톤 및 미래의 10톤급 화물 무인항공기에서 충돌회피는 통합된 시스템 오브 시스템즈 안전 기능(System-of-Systems Safety Function)으로 다루어져야 한다. UTM 조정, 지오펜싱, 기체 탑재 인지, 센서 융합, 궤적 예측, 충돌 탐지, 회피계획, 비행제어, 통신, 사이버보안 및 비상상황 관리(Contingency Management)는 적절한 독립성을 유지하면서 상호 협력해야 한다. 이러한 구조는 정상, 성능 저하 및 예상하지 못한 운용조건에서 자율 화물 항공기가 안전 분리를 유지할 수 있도록 한다.

궁극적인 목적은 충돌 직전에 단순히 반응하는 것이 아니라 항공기 주변에 지속적으로 보호되는 운용 영역(Continuously Protected Operational Envelope)을 유지하는 것이다. 전략적 조정은 예측 가능한 충돌을 예방하고, 전술적 센싱(Tactical Sensing)은 예상하지 못한 위험을 탐지하며, 예측 알고리즘은 조우 상황이 어떻게 변화할지를 판단하고, 필요한 경우 자율제어(Autonomous Control)가 안전한 대응을 실행한다. 이러한 계층이 결합되어 물류 허브, 항만, 공항, 산업지역 및 장거리 운송 회랑(Long-Range Transportation Corridor)에서 확장 가능한 화물 무인항공기 운항을 위한 기반을 제공한다.

## 07.05. UTM Regulatory Compliance

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

UTM 규제 준수(UTM Regulatory Compliance)는 무인항공기(Unmanned Aircraft)가 항공 당국(Aviation Authority)의 요구사항을 충족하면서 관리 공역(Managed Airspace)에 참여할 수 있도록 하는 법적, 운용적, 기술적 및 안전 체계이다. 화물 무인항공기(Cargo UAV)의 경우 항공기 질량, 운항 범위, 자율비행 능력 및 관제 공역(Controlled Airspace)과의 상호작용이 증가하면서 운항 위험과 규제 책임도 함께 증가하므로 규제 준수를 시스템 구조(System Architecture)에 통합해야 한다.

규제 준수는 화물 무인항공기가 운항하게 될 운용개념(Concept of Operations)을 정의하는 것에서 시작된다. 운용자는 예정 비행경로, 고도 범위, 출발 및 목적 시설, 인구 노출(Population Exposure), 공역 등급(Airspace Class), 통신 범위, 기상 한계 및 예상 자율화 수준을 식별해야 한다. 이러한 조건은 항공기 성능, UTM 서비스, 운용 절차 및 안전 완화조치(Safety Mitigation)를 평가하는 기준이 되는 운용영역(Operational Envelope)을 구성한다.

UTM 구조는 항공기 운용자, 원격조종사 또는 감독자(Remote Pilot or Supervisor), UTM 서비스 제공자(UTM Service Provider), 항행기관(Air Navigation Organization), 인프라 운영자(Infrastructure Operator), 항공 당국 사이의 책임을 명확하게 유지해야 한다. 자동화는 승인 확인, 궤적 조정, 모니터링 및 충돌 탐지를 수행할 수 있지만 규제상 책임이 모호해져서는 안 된다. 따라서 각 기능은 누가 정보를 제공하고, 누가 검증하며, 누가 운항 결정을 내리고, 비정상 상황에서 누가 최종 권한을 유지하는지를 정의해야 한다.

항공기 식별(Aircraft Identification)과 등록(Registration)은 규제 추적성(Regulatory Traceability)의 기반을 제공한다. 각 화물 무인항공기는 인정된 항공기 식별정보, 책임 운용자, 구성 상태(Configuration Status), 적용되는 운항 승인과 연계되어야 한다. 디지털 식별정보(Digital Identification Information)를 통해 UTM 서비스와 관계기관은 공역에서 관측된 항공기를 승인된 운항과 연결할 수 있다. 식별정보 관리는 기체 탑재 항공전자시스템(Onboard Avionics), 지상통제국(Ground Control Station, GCS), 기단관리(Fleet Management), 정비 및 운항 기록 전반에서 일관성을 유지해야 한다.

운항 승인(Operational Authorization)은 규제 요구사항과 개별 임무를 연결한다. 출발 전에 운용자는 항공기 식별정보, 비행경로, 고도, 운항 시간대(Time Window), 운용 공간(Operational Volume), 출발 및 목적 위치, 관련 비상상황 정보(Contingency Information)와 같은 필수 정보를 제출한다. UTM 또는 관련 기관 인터페이스는 현재의 공역 제한사항과 적용 규정에 따라 요청을 평가할 수 있다. 이후 승인 상태는 임무계획 및 감독 시스템에 모호함 없이 전달되어야 한다.

지오펜싱(Geofencing)은 규제상의 공역 제한을 기계 판독 가능한 운용 제약조건(Machine-Readable Operational Constraint)으로 변환하여 규제 준수를 지원한다. 비행금지구역, 관제구역, 임시 제한구역, 공항 보호구역, 핵심 인프라 및 비상 공역을 지리적 경계, 고도 및 시간 조건으로 표현할 수 있다. 규제 조건은 출발 후에도 변경될 수 있으므로 임무시스템(Mission System)은 비행 전에 이러한 제한사항을 검증하고 운항 중에도 지속적으로 감시해야 한다.

항공기가 다른 공역 사용자와 적절한 분리(Separation)를 유지해야 하므로 교통 조정(Traffic Coordination)과 충돌회피(Collision Avoidance) 역시 규제 준수의 중요한 요소이다. 전략적 UTM 기능은 비행 전에 궤적 충돌을 식별할 수 있으며, 전술적 탐지 및 회피 시스템(Detect-and-Avoid System)은 운항 중 예상하지 못한 항공기 또는 장애물에 대응한다. 따라서 규제 준수는 네트워크 수준의 교통 서비스와 기체 탑재 안전 기능 사이의 조정에 의존하며 어느 한쪽이 모든 조우 상황을 독립적으로 관리할 수 있다고 가정해서는 안 된다.

명령 및 제어 통신(Command and Control Communication)은 계획된 운항에 필요한 가용성과 성능을 충족해야 한다. 장거리를 운항하는 화물 무인항공기는 셀룰러 통신, 전용 항공통신, 위성통신 또는 여러 개의 이중화 링크(Redundant Link)를 사용할 수 있다. 규제 준수 분석에서는 통신 범위, 지연시간(Latency), 연속성(Continuity), 고장 탐지 및 복구 동작을 고려해야 한다. 주 통신 링크가 손실되면 항공기가 예측할 수 없는 상태에 놓이는 것이 아니라 정의된 성능 저하 상태(Degraded State) 또는 비상상태(Contingency State)로 전환되어야 한다.

항법 성능(Navigation Performance) 역시 승인된 공역과 임무에 적합해야 한다. GNSS, GNSS-RTK, 관성측정장치(Inertial Measurement Unit, IMU) 및 기타 항법 정보원은 기체 탑재 제어와 UTM 보고 기능에 항공기 위치 및 궤적 정보를 제공한다. 시스템 구조는 정확도(Accuracy), 무결성(Integrity), 가용성(Availability), 동기화(Synchronization)를 감시하여 항법 성능 저하를 인식할 수 있어야 한다. 필요한 대응에는 더 큰 분리여유, 경로 제한, 복귀, 대기(Holding), 우회(Diversion) 또는 비상착륙이 포함될 수 있다.

비상상황 절차(Contingency Procedure)는 규제 준수의 주요 부분이다. 명령 링크 손실, 항법 성능 저하, 추진계 고장, 에너지 부족, 악천후, 센서 고장, UTM 통신 손실 또는 승인된 경로를 따를 수 없는 상황에는 사전에 정의된 대응이 있어야 한다. 항공기, GCS 및 UTM 인터페이스는 이러한 상태를 일관되게 표현하여 운용자와 주변 공역 참여자가 항공기의 상태와 예상되는 행동을 이해할 수 있도록 해야 한다.

비상 권한(Emergency Authority)은 정상적인 운항 승인과 명확하게 구분되어야 한다. 즉각적인 안전 위협에 직면한 화물 무인항공기는 항공기와 지상의 사람을 보호하기 위해 승인된 비행궤적, 고도 또는 지오펜스 제약조건에서 이탈해야 할 수 있다. 시스템 구조는 이러한 이탈이 언제 허용되는지, 비상상태가 어떻게 선언되는지, 외부 서비스에 어떻게 통보되는지, 그리고 전체 과정이 이후 규제 검토(Regulatory Review)를 위해 어떻게 기록되는지를 정의해야 한다.

UTM 운항은 신뢰할 수 있는 디지털 정보에 의존하므로 사이버보안(Cybersecurity)은 규제 보증(Regulatory Assurance)에 직접적으로 기여한다. 항공기 식별정보, 운항 승인, 위치 보고, 지오펜스 갱신, 교통 정보 및 명령 관련 데이터는 승인되지 않은 변경이나 위장(Impersonation)으로부터 보호되어야 한다. 인증(Authentication), 무결성 검증(Integrity Checking), 필요한 경우의 암호화(Encryption), 자격증명 관리(Credential Management), 접근통제(Access Control), 안전한 소프트웨어 업데이트 및 감사 로그(Audit Logging)는 규제 결정이 유효한 정보에 기반한다는 신뢰를 지원한다.

소프트웨어 및 하드웨어 형상관리(Configuration Control)는 규제 준수 증거가 정의된 항공기 및 시스템 구성에 적용되므로 필수적이다. 비행제어 소프트웨어, 항법 알고리즘, 통신장비, 센서, UTM 인터페이스 또는 안전 매개변수의 변경은 운항 동작에 영향을 미칠 수 있다. 따라서 형상관리(Configuration Management)는 승인된 버전을 식별하고, 업데이트를 통제하고, 변경사항을 문서화하며, 변경으로 인해 추가적인 검증(Verification), 유효성 확인(Validation) 또는 규제 평가가 필요한지를 판단해야 한다.

검증 및 유효성 확인(Verification and Validation)은 규제 요구사항이 올바르게 구현되었다는 증거를 제공한다. 시험에는 정상 운항, 경계조건(Boundary Condition), 통신 고장, 항법 성능 저하, 센서 고장, 지오펜스 갱신, 교통 충돌, 비상상태 전환 및 복구 절차가 포함되어야 한다. 시뮬레이션(Simulation), 소프트웨어 인 더 루프(Software-in-the-Loop), 하드웨어 인 더 루프(Hardware-in-the-Loop), 지상시험, 통제된 비행시험 및 운용 실증을 통해 고위험 화물 운항이 승인되기 전에 단계적으로 증거를 구축할 수 있다.

로그 기록(Logging)과 추적성(Traceability)은 관계기관과 운용자가 임무 중 시스템이 어떻게 동작했는지를 재구성할 수 있도록 한다. 관련 기록에는 승인 메시지, 항공기 위치, 비행궤적, 지오펜스 버전, 교통 주의정보(Traffic Advisory), 통신 상태, 시스템 건전성(System Health), 운용자 명령, 자율 의사결정, 비상 이벤트 및 소프트웨어 구성이 포함될 수 있다. 여러 독립적인 시스템에서 정보가 생성되는 경우 정확한 타임스탬프와 동기화된 기록(Synchronized Record)이 특히 중요하다.

지상통제국(Ground Control Station, GCS)은 감독 운용자에게 규제 및 운항 정보를 제공하므로 주요 규제 준수 인터페이스(Compliance Interface)이다. 운항 승인 상태, 활성 제한사항, 통신 건전성(Communication Health), 항법 품질, 교통 충돌, 비상상태 및 경로 이탈이 불필요한 모호성 없이 표시되어야 한다. 인터페이스는 적시에 의사결정을 지원하면서 운용자가 현재의 운항 제한조건과 충돌하는 명령을 인지하지 못한 채 수행하는 것을 방지해야 한다.

하나의 조직이 다수의 화물 무인항공기를 운용하면 기단관리(Fleet Management)에 추가적인 규제 준수 요구사항이 발생한다. 시스템은 각 항공기의 승인 상태, 항공기 구성, 운용자 할당, 정비 상태, 비행경로 및 운항 상태를 독립적으로 관리해야 한다. 자동 일정관리(Automated Scheduling)와 임무 할당(Mission Allocation)은 필요한 승인, 정비 조건, 통신 능력 또는 인프라 자원을 사용할 수 없는 항공기가 임무에 배정되는 것을 방지해야 한다.

버티포트(Vertiport), 공항, 물류 허브(Logistics Hub) 및 지원 인프라도 규제 준수 환경의 일부가 된다. 출발 및 도착 절차는 보호된 운용 공간, 착륙 패드 가용성, 장애물 안전거리(Obstacle Clearance), 지상 안전구역, 화물 취급, 충전 또는 연료보급 상태, 비상대응 능력에 따라 달라질 수 있다. 항공기, 인프라, 기단 시스템 및 UTM 서비스 사이의 디지털 조정은 승인된 공역 운항이 실제 목적지의 물리적 조건과도 호환되도록 지원한다.

화물 무인항공기의 크기와 운항 범위가 증가할수록 기존 항공교통관리(Air Traffic Management, ATM)와의 상호운용성(Interoperability)은 더욱 중요해진다. 지역 또는 장거리 임무는 UTM 또는 유스페이스 환경과 기존 항공 절차에 따라 관리되는 관제 공역 사이를 전환할 수 있다. 규제 준수 구조는 이러한 전환 과정에서 상충되는 지시나 불명확한 권한을 발생시키지 않으면서 항공기 식별정보, 비행 의도, 승인 상태, 교통 정보 및 운항 책임을 유지해야 한다.

국제 운항(International Operation)은 국가와 지역에 따라 규제 체계, 공역 서비스, 통신 요구사항, 데이터 정책 및 운항 승인 절차가 다를 수 있기 때문에 또 다른 수준의 복잡성을 추가한다. 미래의 장거리 화물 운송 네트워크는 안정적인 항공기 수준의 안전 기능(Aircraft-Level Safety Function)과 구성 가능한 규제 규칙 및 서비스 인터페이스를 분리해야 한다. 이를 통해 모든 안전 필수 하위시스템을 다시 설계하지 않고도 동일한 기본 항공기 구조를 서로 다른 국가 또는 지역의 운항환경에 적용할 수 있다.

대형 화물 무인항공기의 규제 준수는 항공기의 위험과 운항 결과에 비례해야 한다. 2.5톤, 5톤 또는 10톤급 자율 화물 항공기에 경량 드론을 위해 개발된 가정을 단순하게 적용할 수는 없다. 높은 운동에너지(Kinetic Energy), 긴 정지 및 기동거리, 더 큰 운용 공간, 복잡한 추진시스템 및 기존 항공체계와의 상호작용으로 인해 더욱 강력한 안전 증거(Safety Evidence), 이중화(Redundancy), 비상계획, 시스템 모니터링 및 운항 거버넌스(Operational Governance)가 필요하다.

따라서 규제 준수는 운항 개시 전에 한 번만 입증하는 것이 아니라 항공기의 전체 수명주기(Aircraft Lifecycle)에 걸쳐 유지되어야 한다. 제조 형상, 소프트웨어 업데이트, 정비, 부품 교체, 운항 변경, 사고 조사 결과 및 변화하는 공역 규정은 지속적인 규제 준수에 영향을 줄 수 있다. 정기적인 검토와 통제된 변경관리(Controlled Change Management)를 통해 항공기와 UTM 생태계가 발전하더라도 승인된 안전 및 운항 기준선(Safety and Operational Baseline)을 유효하게 유지할 수 있다.

완전한 UTM 규제 준수 구조(UTM Regulatory Compliance Architecture)는 운항 승인, 식별, 지오펜싱, 교통 조정, 탐지 및 회피(Detect-and-Avoid), 통신, 항법, 사이버보안, 비상상황 관리, 형상관리, 시험, 로그 기록, 기단 감독, 인프라 통합 및 ATM 상호운용성을 통합한다. 규제 준수는 기술 설계, 운용 절차, 디지털 기록 및 명확하게 할당된 책임에 의해 지속적으로 유지되는 시스템 속성(Continuous System Property)이 된다.

미래의 2.5톤, 5톤 및 10톤급 화물 무인항공기 네트워크에서 이러한 통합적 접근은 실험적 비행에서 반복 가능한 상용 운항(Repeatable Commercial Operation)으로 발전하기 위한 기반을 제공한다. 규제 요구사항은 시스템 제약조건으로 변환되고 시험을 통해 검증되며 임무 중 적용되고 UTM과 기체 탑재 시스템을 통해 감시되며 추적 가능한 기록으로 보존된다. 그 결과 더 넓은 항공 시스템과의 책임 있고 예측 가능한 통합을 유지하면서 점차 높은 수준으로 자율화되는 화물 운송을 지원할 수 있는 구조가 구축된다.
