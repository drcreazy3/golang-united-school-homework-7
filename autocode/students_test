package coverage

import (
	"os"
	"testing"
	"time"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW

func TestLen(t *testing.T) {
	people := People{Person{firstName:"Sergei", lastName: "Sevkovich", birthDay: time.Date(1988, 6, 6, 11, 30, 0, 0, time.Local)}}
	
	tData := map[string]struct {
		P People
		Expected int
	}{
		"empty":          {P:People{}, Expected: 0},
		"some values":    {P:people, Expected: 1},
	}

	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			actual := v.P.Len();
			if actual != v.Expected {
				t.Errorf("[%s] expected: %d, actual %d", name, v.Expected, actual)
			}
		})
	}

}

func TestLess(t *testing.T) {
	people := People{
		Person{firstName:"Sergei", lastName: "Sevkovich", birthDay: time.Date(1988, 6, 6, 11, 30, 0, 0, time.Local)},
		Person{firstName:"Barak", lastName: "Obama", birthDay: time.Date(1961, 8, 4, 12, 00, 0, 0, time.Local)},
		Person{firstName:"Barak", lastName: "Abama", birthDay: time.Date(1961, 8, 4, 12, 00, 0, 0, time.Local)},
		Person{firstName:"Aarak", lastName: "Abama", birthDay: time.Date(1961, 8, 4, 12, 00, 0, 0, time.Local)},
	}
	
	tData := map[string]struct {
		P1 int
		P2 int
		Expected bool
	}{
		"diff birthdays p": {P1:0, P2:1, Expected:true},
		"diff birthdays n": {P1:1, P2:0, Expected:false},
		"same birthdays but different last name p": {P1:2, P2:1, Expected:true},
		"same birthdays but different last name n": {P1:1, P2:2, Expected:false},
		"same birthdays but different first name p": {P1:3, P2:2, Expected:true},
		"same birthdays but different first name n": {P1:2, P2:3, Expected:false},
	}

	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			t.Parallel()
			actual := people.Less(v.P1, v.P2)
			if actual != v.Expected {
				t.Errorf("[%s] expected: %t, actual %t", name, v.Expected, actual)
			}
		})
	}
}

func TestSwap(t *testing.T) {
	people := People{
		Person{firstName:"Sergei", lastName: "Sevkovich", birthDay: time.Date(1988, 6, 6, 11, 30, 0, 0, time.Local)},
		Person{firstName:"Barak", lastName: "Obama", birthDay: time.Date(1961, 8, 4, 12, 00, 0, 0, time.Local)},
	}


	tData := map[string]struct {
		P1 int
		P2 int
	}{
		"swap": {P1:0, P2:1},
	}

	for name, tcase := range tData {
		v := tcase
		t.Run(name, func(t *testing.T) {
			oldP1 := people[v.P1]
			oldP2 := people[v.P2]
			people.Swap(v.P1, v.P2)

			if oldP1 != people[v.P2] || oldP2 != people[v.P1]  {
				t.Errorf("Can not swipe items")
			}
		})
	}
}