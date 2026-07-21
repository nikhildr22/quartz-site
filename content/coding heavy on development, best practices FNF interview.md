```cs
interface IProductRepository{
	int AddProduct(ProductModel model);
	Product GetProduct(int id);
}

ProductRepository : IProductRepository{

	public int AddProduct(ProductModel model){
		// Logic to add product and return id
	}
	
	Product GetProduct(int id){
		// Logic to return Product 
	}
}

Public class ProductManagementService{
	private IProductRepository _productRepository;
	
	ProductManagementService(IProductRepository repository){
			_productRepository = repository;
	}
	
	Public GetProductDetails(int id){
		_productRepository.GetProduct(id);
	}
	
}

// Program.cs
builder.Services.AddSigleton<IProductRepository, ProductRepository>();




//////////
Banking -> account details -> transfer money -> amount > 0;
// frontend -> get account and then transfer, security

// Controller
public GetAccountController : ControllerBase{
	private IAccountService _service;
	GetAccountDetails(IAccountService service){
		_service = service;
	}
	
	[Authorize]
	[HTTPGet('[action:/id'])
	public async Task<ActionResult<AccountModel>> GetAccountDetailsAsync(Guid id, CancellationToken cancellationToken){
		return Ok(await _service.GetAccountDetailsAsync(id, cancellationToken);
	}
	
	[Authorize]
	public async Task<ActionResult<bool>> TransferAmountAsync(AmountTransferModel model, CancellationToken cancellationToken){
		var result = _service.TransferAmountAsync(model, cancellationToken);
		return Ok(result);
	}
	
	Authorize
	public async Task<ActionResult<List<AccountListModel>> SearchAccountsAsync(string name, CancellationToken cancellationToken){
		return _service.SearchAccountsAsync(name, cancellationToken);
	}
	
	
	
}


// Data Models Folder
public class AccountBaseModel{
	public string AccountHolderFullName {get; set;}
	public string AccountId {get; set;}
}
AccountListModel : AccountBaseModel {
	
}

AmountTransferModel{
	public Guid SenderAccountId {get; set;}
	public Guid RecipientAccountId {get; set;}
	public double Amount {get; set;}

}

//  Interfaces
IAccountService{
	Task<AccountModel> GetAccountDetailsAsync(Guid id, cancellationToken);
	Task<bool> TransferAmountAsync(AmountTransferModel model, CancellationToken cancellationToken);
	Task<List<AccountListModel> SearchAccountsAsync(string name, CancellationToken cancellationToken);
}

// Should add Fluent vallidation to validate AmountTransferModel

// Service Implementation
Public AccountService : IAccountService{
	private IDbContext _dbContext;
	AccountService(IDbContext dbContext){
		_dbContext = dbContext;
	}
	
	public async Task<AccountModel> GetAccountDetailsAsync(Guid id, cancellationToken){
		return await _dbContext.Accounts
				.Select(account => new AccontModel(){
					AccountHolderFullName = account.AccountHolderFullName,
					AccountId = account.AccountId;
				}
				.singleAsync(i => i.id == id, cancellationToken);
	}
	
	public Task<bool> TransferAmountAsync(AmountTransferModel model, CancellationToken cancellationToken){
		if(model.Amount <=0){
			return false;
		}
		
		var recipentAccount = _dbContext.Accounts.
					.SingleAsync(account => account.id == model.receipeintId);
					
		var senderAccount =  await _dbContext.Accounts
						.SingleAsync(account => account.id == model.senderId);
						
		recipentAccount.Amount += model.Amount;
		senderAccount.Amount -= model.Amount;
		
		await _dbContext.SaveChangesAsync(cancellationToken);
		return true;
	}
	Task<List<AccountListModel> SearchAccountsAsync(string name, CancellationToken cancellationToken){
		return await _dbContext.Accounts
						.ToListAsync(account => new AccountListModel(){name, id});
	}
}

// Program.cs
Inject IAccountService as scoped



/// Front End

// Components

// imports
// Main transfer amount window component
@Component{
	selector: 'anmount-transfer-overview-component',
	Templates:[],
	Styles: [],
	Imports : [AccountAutoCompleteComponent],
	standalone: true;
}

export class AmountTranferOverViewComponent implements OnDestroy {
	constuctor(AccountService : accountService)

	tranferStatus = null;
	
	 formGroup : new FormGroup{
		senderId: string not null, required,
		receieverId: string not null, required,
		Amount: number, Validations(required), shouldBeGreaterThan0
	}
	
	protected onTransferAmountBtnClick($event event){
		if(this.formGroup.Valid){
			accountService.TransferAmount(this.formGroup.getRawValue())
			.UnSubscribeOnDestroy(this)
			.Subscibe((result)=>{
				tranferStatus = result;
			})
		}
	}
	
	protected OnAccountSelected(string accountId, string acccountType){
		this.form
	}
	
}

// HTML

<account-autocomplete-search-component > </account-autocomplete-search-component>





// Search Account Component - Auto complete search




//TS file
@Component{
	selector: 'account-autocomplete-search-component',
	Templates:[],
	Styles: [],
	Imports : [],
	standalone: true;
}

export class AccountAutoCompleteComponent implements OnInit{
	@Input searchString = '';
	@output selectedAccountId;
	protected accountList
	
	ngOninit(){
		
	}
	
	OnAccountSelect($event event){
		selectedAccountId.emit(event.id);
	}
	
	onSearchBtnClick(){
		
	}
	

}

// HTML will have select component, on select event handler calling OnAccountSelect


------------------
top 3 custombers who tranferred highest total amounnt

select SUM(amount) from Customers
GroupBy customerId
Having 

Transfers.
.GroupBy(transfer => transfer.senderId)
.Select(group => group.Sum(group.amount))
.Take(3)
OrderByDescending(transfer =>










```