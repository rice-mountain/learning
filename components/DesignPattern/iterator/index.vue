<template>
  <div>
    <h2>Iterator Comp</h2>

  </div>
</template>

<script setup lang="ts">
  class Patient {
    constructor(public id:number, public name: string){}
  }

  interface IIterator {
    hasNext(): boolean
    next(): void | Patient;
  }

  interface Aggregate {
    getIterator(): IIterator
  }

  class WaitingRoom implements Aggregate {
    private patients: Patient[] = [];
    
    getPatients(): Patient[] {
      return this.patients;
    }

    getCount(): number {
      return this.patients.length
    }

    checkIn(patient: Patient) {
      this.patients.push(patient);
    }

    getIterator(): IIterator {
        return new WaitingRoomIterator(this)
    }
  }

  class WaitingRoomIterator implements IIterator {
    private position: number = 0

    constructor(private aggregate: WaitingRoom) {}

    hasNext(): boolean {
      return this.position < this.aggregate.getCount();
    }

    next() {
      if (!this.hasNext()) {
        console.log("患者がいません")
        return
      }
      const patient = this.aggregate.getPatients()[this.position];
      this.position++
      return patient;
    }
  }

  function run() {
    const waitingRoom = new WaitingRoom();
    waitingRoom.checkIn(new Patient(1, 'yamada'))
    waitingRoom.checkIn(new Patient(2, 'suzuki'))
    waitingRoom.checkIn(new Patient(3, 'tanaka'))

    const iterator = waitingRoom.getIterator();
    console.log(iterator.next())
    console.log(iterator.next())
    console.log(iterator.next())
    console.log(iterator.next())
  }

  run()
</script>
