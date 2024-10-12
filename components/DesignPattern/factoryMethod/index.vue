<template>
  <div>
    <h2>FactoryMethod Comp</h2>
  </div>
</template>

<script setup lang="ts">

abstract class CreditCard {
  constructor(public owner: string) {}

  getOwner(): string {
    return this.owner;
  }

  abstract getCardType(): string;
  abstract getAnnualCharge(): number
}

class Platinum extends CreditCard {
  override getCardType(): string {
      return "Platinum"
  }
  override getAnnualCharge(): number {
      return 30000
  }
}

class Gold extends CreditCard {
  override getCardType(): string {
      return "Gold"
  }
  override getAnnualCharge(): number {
      return 10000
  }
}

abstract class CreditCardFactory {
  abstract createCreditCard(owner: string): CreditCard;
  abstract registerCreditCard(creditCard: CreditCard): void;

  create(owner:string): CreditCard {
    const creditCard = this.createCreditCard(owner);
    this.registerCreditCard(creditCard)
    return creditCard;
  }
}

const creditCardDatabase: CreditCard[] = []

class PlatinumCreditCardFactory extends CreditCardFactory {
  override createCreditCard(owner: string): CreditCard {
      return new Platinum(owner);
  }
  override registerCreditCard(creditCard: CreditCard): void {
      creditCardDatabase.push(creditCard);
  }
}

class GoldCreditCardFactory extends CreditCardFactory {
  override createCreditCard(owner: string): CreditCard {
      return new Gold(owner);
  }
  override registerCreditCard(creditCard: CreditCard): void {
      creditCardDatabase.push(creditCard);
  }
}

function run() {
  const platinumCardFactory = new PlatinumCreditCardFactory();
  const platinumCard = platinumCardFactory.create("tanaka")
  console.log(platinumCard)

  const goldCardFactory = new GoldCreditCardFactory();
  const goldCard = goldCardFactory.create("suzuki")
  console.log(goldCard)

  console.log(creditCardDatabase)
}

run();
</script>
