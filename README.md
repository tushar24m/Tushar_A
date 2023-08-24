# bank-record-storage-system-
Certainly! In layman's terms, the project you're looking at involves creating a secure and trustworthy system for keeping records of financial transactions in a bank. Imagine you're using a special digital notebook that ensures that no one can tamper with the records you write down.

Here's how it works:

1. Creating a Record: Whenever a transaction happens, like when money is sent from one person to another, we note down who sent it (sender), who received it (receiver), and how much money was involved (amount). These are like the details you fill in a form when you send money through a banking app.
                                    @dataclass
                                class Record:
                                    sender: str
                                    receiver: str
                                    amount: float

2. a)Blocks for Security: Instead of writing each transaction on its own, we group several transactions together in a 'block'. Each block is like a page in a book, and it's linked to the previous page (block) to make sure nobody can secretly change any of the pages.
   b)Adding New Transactions: When you want to add a new transaction to the record, you enter the sender's name, receiver's name, and the amount. This information is put into a new block and connected to the previous block to form a secure chain.
                                        @dataclass
                                    class Block:
                                        record: Record
                                        # ... other attributes ...
                                    
                                        def hash_block(self):
                                            # ... hash calculation ...

3. a) Checking and Securing: To make sure nobody messes with the records, the system uses a special code (hash) to 'lock' each block. This code depends on all the information in the block, so if even a tiny detail changes, the code will be completely different.
   b)Validation: You can imagine it like a puzzle – the computer has to solve a puzzle to add a new block. This ensures that the records are accurate and trustworthy. If someone tries to change anything in a previous block, the puzzle won't work anymore, and everyone will know that something fishy is going on.
   c) User-Friendly Interface: The whole process is made easy through a simple website-like interface. You just need to type in who sent money, who received it, and how much. The system then creates a secure record for you.

                            sender = st.text_input("Enter Sender:")
                            receiver = st.text_input("Enter Receiver:")
                            amount = st.number_input("Enter Transaction Amount:")
                            
                            if st.button("Add Block"):
                                prev_block = pychain.chain[-1]
                                prev_block_hash = prev_block.hash_block()
                            
                                new_block = Block(
                                    record=Record(
                                        sender=sender,
                                        receiver=receiver,
                                        amount=amount),
                                    sender=sender,
                                    receiver=receiver,
                                    amount=amount,
                                    creator_id=42,
                                    prev_hash=prev_block_hash
                                )
                            
                                pychain.add_block(new_block)
                                st.balloons()

5. Testing and Validating: You can test the system by creating transactions and adding them to the record. The system also checks if the record is valid – just like how your teacher checks if your answers are correct. If everything is correct, you'll see a message that the record is valid.
                                  pychain_df = pd.DataFrame(pychain.chain).astype(str)
                                  st.write(pychain_df)
                                  
                                  difficulty = st.sidebar.slider("Block Difficulty", 1, 5, 2)
                                  pychain.difficulty = difficulty
                                  
                                  st.sidebar.write("# Block Inspector")
                                  selected_block = st.sidebar.selectbox(
                                      "Which block would you like to see?", pychain.chain
                                  )
                                  
                                  st.sidebar.write(selected_block)
                                  
                                  if st.button("Validate Chain"):
                                      st.write(pychain.is_valid())

This project essentially builds a smart and secure system for keeping track of financial transactions in a bank, making sure everything is accurate and cannot be tampered with. It's like a high-tech version of a super-safe ledger that ensures your money is in safe hands!

PACKAGE REQUIREMENTS-
pip install x where x is the below listed packages
  1. Python 3.7.13
  2. pandas 1.3.5
  3. streamlit 1.13.0

REFERNECES
1. https://phemex.com/academy/blockchain-validator-process
2. https://en.bitcoin.it/wiki/Mining#The_Difficulty_Metric

