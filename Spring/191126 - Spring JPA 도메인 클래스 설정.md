도메인 클래스에 다음과 같이 DB테이블과 매핑 시키는 것이 jpa의 핵심은 듯함

jpa에서 DDD(Domain Driven Design) 방식을 위한 기본 설정으로 보임

직관적인 설계를 지향

```java
@Entity
@Table(name = "EMPLOYEE")
public class Employee {

	@Id
	@Column(name = "EMPLOYEE_ID")
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;

	@Column(name = "EMPLOYEE_NUM")
	private String employeeNumber;

	@Column(name = "NAME")
	private String name;

	@Embedded
	@AttributeOverrides({ @AttributeOverride(name = "address1", column = @Column(name = "HOME_ADDR1")),
			@AttributeOverride(name = "address2", column = @Column(name = "HOME_ADDR2")),
			@AttributeOverride(name = "zipcode", column = @Column(name = "HOME_ZIPCODE")) })
	private Address address;

	@Column(name = "BIRTH_YEAR")
	private int birthYear;

	@ManyToOne
	@JoinColumn(name = "TEAM_ID")
	private Team team;

	@Temporal(TemporalType.DATE)
	@Column(name = "JOINED_DATE")
	private Date joinedDate;

}
```

